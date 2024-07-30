# Compiling a Custom arduino-esp32 Build

We'll be building arduino-esp32 release 2.x with IDF 4.4.x, which is required for S3 and other modern ESP32 variants.

This requires MacOS or Linux. If you're using Windows, then the Windows Subsystem for Linux works great too as it's Ubuntu based, which matches the docs perfectly and works flawlessly with this.

1. Setup your environment as per the docs and give the entire doc a quick review:
   * https://docs.espressif.com/projects/arduino-esp32/en/latest/lib_builder.html
2. Clone the library builder to local disk:
   * `git clone -b release/v4.4 https://github.com/espressif/esp32-arduino-lib-builder`
   * It may also be worth forking this to your own repo to track your local changes, YMMV.
3. Fork https://github.com/espressif/arduino-esp32 to your own GitHub account.
   * I also changed my default branch on my GitHub repo to `release/v2.x` to make things easier.
   * This is where you'll be pulling your shiny new ardino-esp32 build from eventually.
4. Clone your fork of arduino-esp32 to local disk:
   * `git clone -b release/v2.x https://github.com/YOUR-GITHUB/arduino-esp32/`
   * You'll need this "working copy" as the baseline for a functional repo with your new build added.
5. Now you should be ready to build!
6. Change to your `esp32-arduino-lib-builder` directory and run `./build.sh` and it should make you a fully default build for all boards and the current IDF for 4.4.x!
  * ...but if you're reading this, you likely don't want that - and it takes a LONG time even on a fast system.
  * ...and it's likely using an IDF 4.4.x version you don't want.
  * ...but it's a good test for making sure your build environment is working, even if you cancel it after a few iterations. 

## Gotchas

There's several things that are not obvious when building arduino-esp32 - like "how do I make my customizations actually get used in the build?" 

I'll be using the ESP32-S3 as the build target here, but the same general idea works for other boards.

Run the menuconfig for your board variant:
  * `./build.sh -t esp32s3 -b menuconfig` and set your options
  * Generally, you only will want to modify things in "Arduino Configuration" and the menus below it (Arduino TinyUSB, Compiler options, etc)
  * This will create an `sdkconfig` file in the root of `esp32-arduino-lib-builder`

![WindowsTerminal_Ft6C7pnL2r](https://github.com/user-attachments/assets/e2c5ee91-e730-4287-8e80-cd1c9837b4dc)

This file is functionally useless because the build system will use `configs/defconfig.common` with `configs/defconfig.esp32s3` and then add your `sdkconfig` file - which means most of your modifications will be overwritten by the defaults and we do not want that. 

To get your new build to use your menuconfig created build file:

1. Change to your `esp32-arduino-lib-builder` folder.
2. `cd configs`
3. `cp defconfig.common defconfig.common.org` to make a backup
4. `cp defconfig.esp32s3 defconfig.esp32s3.org` to make a backup
5. `rm defconfig.esp32s3` to get rid of the S3 defaults
6. `touch defconfig.esp32s3` to make a blank file so nothing complains during the build
7. `cp ../sdkconfig defconfig.common` to put your options into the build file.
8. ...and now you're ready to build!
9. `./build.sh -c /path/to/your/arduino-esp32/ -t esp32s3`
   * This will use whatever IDF v4.4.x is current. See "Using a different v4.4.x version of the IDF" below for how to override this.
10. This should build the ESP32-S3 build with your options and copy it into the correct spot in `/path/to/your/arduino-esp32/`

There are other ways to do this, but with this method your previous choices are reflected as the default options when you run `menuconfig` again. 

**NOTE**: You could make a blank `defconfig.common` file and `cp ../sdkconfig defconfig.esp32s3` if you want to make different board configs with menuconfig. 

In order to undo this if you things aren't working and you can't remember which options you changed, just `cp defconfig.common.org defconfig.common` and `cp defconfig.esp32s3.org defconfig.esp32s3` and then `menuconfig` will start with the original "sane" defaults again.  

### Using a different v4.4.x version of the IDF

This is useful because IDF v4.4.7 and above have differences that might cause WLED to break without some patching on your part, at least in MoonModules WLED. 

1. Go to https://github.com/espressif/esp-idf/releases
2. Scroll/search until you find the IDF version you want - I'm using 4.4.6 here.

![chrome_cWijfbLctd](https://github.com/user-attachments/assets/a551ec76-bdb7-48d2-ad47-631630ef8ebd)

Note the commit and the version tag, then run your build with those included:

Build with `./build.sh -I v4.4.6 -i 3572900 -c /path/to/your/arduino-esp32/ -t esp32s3` instead of `./build.sh -c /path/to/your/arduino-esp32/ -t esp32s3`

### Building additional/other targets

**UNTESTED**: You should be able to repeat the steps above for a different target and it'll copy those to the appropriate directories in `/path/to/your/arduino-esp32/` to add them to your repo on commit+push.

It does seem easier to build things one at a time, and only the boards you actually use - because it takes a LONG TIME to build all the targets.  

### Using -O2 to build

IF you selected `Compiler Options ---> Optimization Level --->  Optimize for performance (-O2)` in menuconfig (which I think you should try!) you may need to adjust `esp32-arduino-lib-builder` to get it to build, due to some bugs in how it treats compiler some warnings as errors when they are not.

1. Change to your `esp32-arduino-lib-builder` folder.
2. `nano esp-idf/CMakeLists.txt`
3. In the `if(NOT BOOTLOADER_BUILD)` block, in the ` elseif(CONFIG_COMPILER_OPTIMIZATION_PERF)` block, set it like this:
```
    elseif(CONFIG_COMPILER_OPTIMIZATION_PERF)
        list(APPEND compile_options "-O2")
        list(APPEND compile_options "-Wno-stringop-truncation")
        list(APPEND compile_options "-Wno-stringop-overflow")
        list(APPEND compile_options "-Wno-maybe-uninitialized")
        list(APPEND compile_options "-ffast-math")
```
If you really want to experiment, you can change `-O2` to `-O3` or even `-Ofast` but only `-O2` seems to work for everything in my custom builds. 

If a build is failing due to a compiler warning, you can edit the above block in `esp-idf/CMakeLists.txt` to add more `-Wno-compiler-warning-that-is-failing` lines to suppress and perhaps get past the particular warning that's causing the build to fail. _**All options DO need to be added one-per-line or it breaks the build system.**_

## Deploying this so you can use it

After you've done all this and `./build.sh -I v4.4.6 -i 3572900 -c /path/to/your/arduino-esp32/ -t esp32s3` (or whatever) has succeeded, you can now commit this to your repo and use it in PlatformIO:

1. `cd /path/to/your/arduino-esp32/`
2. `git commit -a`
3. Add your commit message.
4. `git push`
5. You should now have a commit in your repo with your new build!

In your PlatformIO build for your board:
```
platform_packages = platformio/framework-arduinoespressif32 @ https://github.com/YOURUSER/arduino-esp32.git#release/v2.x @ 2.0.17+sha.{commit}
  toolchain-riscv32-esp@~12.2
  toolchain-xtensa-esp32s3@~12.2
board_build.arduino.upstream_packages = no
```
The "{commit SHA}" is a good way to tell PIO to redownload your new modified code as you create and commit new builds. This is 7 characters and shown in your GitHub account with the last commit you did. (Weirdly if you look at your `git push` output it'll show 8 characters - you can just use the first 7 and drop the last character.)

The "toolchain" lines are entirely optional - I'm using a newer compiler here in testing. YMMV, etc.

Version 2.0.17 is the current version as of wiring this, but that can/will likely change in the future, so adjust accordingly. If you change the underlying IDF version, this version won't change automatically - and it doesn't really matter. If you want to be very correct, you can edit `arduino-esp32/package.json` with the correct version of arduino-esp32 for your IDF (with IDF v4.4.6 it should be 2.0.14, for example), or whatever custom version you want it to be. 

You can figure out the IDF to arduino-esp32 version mapping by looking thru https://github.com/espressif/arduino-esp32/releases if you really want everything to be correct, even if it doesn't actually matter in your actual build in PIO. 
