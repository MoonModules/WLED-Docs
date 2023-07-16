---
title: Release notes v0.14.0-b25
hide:
  # - navigation
  # - toc
---

[MoonModules v0.14.0-b25, release July 15th 2023](https://github.com/MoonModules/WLED/releases/tag/v0.14.0.b25)

This WLED MM release is based on latest stable dev of WLED AC (June 2, 2023). We have also added a few stability patches that arrived in WLED AC after June 2nd. 
As WLED AC is undergoing a lot of changes, MoonModules built in a longer delay then normal to keep up with upstream until latest upstream is well tested.

Below an overview of major MoonModules specific changes and new features.

## Full Bright Preview
7 July 2023

By @Softhack007

Instead of dimming down, the preview always shows at max brightness - even when the global brightness slider for your LEDs is set to a low value. 

<img width="40%" alt="Full Bright Preview" src="https://github.com/MoonModules/WLED-Docs/assets/91616163/fe32af8f-c4b7-4932-bc1d-a24567547e98"> 

## AnimARTrix Usermod - 2D effects

29 Jun 2023

By @Netmindz

Usermod to allow access to the [AnimARTrix](https://github.com/StefanPetrick/animartrix) 2D effects by [@StefanPetrick](https://github.com/StefanPetrick), all the effect names are prefixed with Y to group them at the bottom of the list. Animation speed can be controled by slider.

## WLED Instances
May 2023

Refactor of the Nodes popup

<img width="1042" alt="New Nodes Popup" src="https://github.com/MoonModules/WLED-Docs/assets/91013628/8e156fd5-9afb-42fc-ac63-215788bd6c11">

* Set on/off
* Show more info of instance
* DDP all: add all found nodes as Led outputs (see led preferences screen), by this the leds of others nodes as added as leds to your node and you can control them from this one node. Note: Might not scale up to 10's of nodes due to network traffic 

## Under-the-hood: Speedups, Bugfixes and improved Stability

### Effect core speedups
1 July 2023 (audio fastpath, part 1)

Some effects will run up to 60% faster now.
A lot of minor speedups to effect core routines were added. Additionally, FastLED color handling code was updated to release 3.6.0.

* up to 220 FPS were measured with 160 LEDs per pin; for max speed, use 2-4 LED pins with your fixture (ws2812b), each driving 150-300 LEDs.
* soundreactive effects were optimized to support high FPS.
* At high FPS (>100), soundreactive effects seem to "flow" with the music now. Try to set the speed slider to 255 in `pixelwave`, `freqmatrix` or `DJ Light`.

<p>
<img width="60%" alt="Configuring high FPS" src="https://github.com/MoonModules/WLED-Docs/assets/91616163/b4d3070b-e7d7-414c-a9b9-5034895c9e5f"> &nbsp;
<img width="50%" alt="Sound Flows" src="https://github.com/MoonModules/WLED-Docs/assets/91616163/7aee247e-cbd6-41c6-a0d1-333c0d58041c">
</p>


### Auto Brightness Limiter works again
30 June 2023

By @Softhack007

Auto Brightness Limiter bugfixes (from WLED AC) are included in this release. 


### Improved Stability
1 June 2023

By @Troy and @Softhack007 and @ewowi

WLEDMM internal memory handling was optimized and improved for reliability. Loading of ledmaps was optimized to prevent repeated reading of the same file.
As a consequence, large setups (>2500 LEDs) and big ledmaps.json files will work much better.
We recommend using an ESP32 board with PSRAM for large setups, as JSON files will be processed in external PSRAM if available ([PSRAM  enabled firmware build](https://github.com/MoonModules/WLED/releases/download/v0.14.0.b25/WLEDMM_0.14.0-b25.29_esp32_4MB_PSRAM_S.bin) needed).


### Peak unlimited
May 16

by @ewowi

Instead of scaling down on pixels when having lots of leds we lower the peak frame rate so we have WYPIWYG (what you peak is what you get)

## Audio Palette Updates

14 April 2023

By @Netmindz

Fix issues with Audio Responsive Hue being single color and add new Audio Responsive Ramp palette. AR Ramp is designed for use with effects like Fire that expect the palette to start with black, then ramp up

## SoundPressure
7 April 2023

By @Softhack007

<p>
<img width="40%" alt="Gravimeter-Soundpressure" src="https://github.com/MoonModules/WLED-Docs/assets/91616163/37b8b8c2-bc6c-4904-a3ed-3911e93b6b08"> 
<img width="40%" alt="Waverly-Soundpressure" src="https://github.com/MoonModules/WLED-Docs/assets/91616163/b212d861-faf8-4dd7-a665-42e044d7f2e5"> 
</p>

In contrast to "volume", sound pressure level changes with the real loudness, as measured by your microphone. It will climb when you turn music louder, and fall when you turn volume down. You need an I2S digital microphone for soundpressure. 

ARTI-FX, and the Waverly and Gravimeter effects already support sound pressure. More effects to come.
Currently SoundPressure is **not** transmitted to networked devices with "UDP sound sync".


## DMX Input
 
6 April 2023
  
By @Netmindz
  
Do you have existing tranditional wired DMX setup and just want to attach you WLED device like any other fixture? Well now you can.
Same behaviour as existing DMX over ip (ArtNet / e1.31), but now with the stability and realiability without the need to use Ethernet.
  
Note: only currently on the _v4 builds due the esp_dmx library needing the 2.x ESP32-Arduino platform

## Support for pixelArt in ARTI-FX
5 April 2023

Idea by @Stiw47

ARTI-FX can show multiple frames, each stored as a separate json file in <ip>/edit

<video width="400" autoplay><source src="https://user-images.githubusercontent.com/1737159/230075460-6652b18e-23ab-4138-a49c-e919b0bcb639.mov" type="video/mp4"></video>

Program can be found here: https://github.com/MoonModules/WLED-Effects/blob/master/ARTIFX/wled/mario.wled

<img width="314" alt="image" src="https://user-images.githubusercontent.com/91013628/230597209-11415a56-b85e-48c9-87cd-f83742fa87d1.png">

As ARTIFX does not support strings, jsonToPixels only contains a sequence number, the name of the json files is combination of segment name (that should be called mario), sequence number and ".json")
See https://github.com/MoonModules/WLED-Effects/blob/master/ARTIFX/wled/presets.json for how to add mario in presets 

And don't forget to upload latest wledv033.json to <ip>/edit (https://github.com/MoonModules/WLED-Effects/blob/master/ARTIFX/wled/wledv033.json)

## Add ES8388 as Sound Reactive Input type
5 April 2023
  
By @Troy and @Netmindz

<img width="168" alt="image" src="https://user-images.githubusercontent.com/91013628/230325351-fe984cbe-625a-4f51-94d5-d5d79c821259.png">

Can be found in these boards:
[LyraT v4.3](https://espressif-docs.readthedocs-hosted.com/projects/esp-adf/en/latest/design-guide/dev-boards/board-esp32-lyrat-v4.3.html)

<img width="243" src="https://user-images.githubusercontent.com/1737159/230074117-97d75509-5511-47d2-a0c5-87ad622085c1.jpeg">

## Git Log
  
git log mdev --pretty=format:"%h - %ad - %an : %s &b" --date=format-local:"%Y-%m-%d" --since="2023-04-02"

```
c0a0f66a - 2023-04-30 - Frank : trying to revive github ci build for new MCUs (#38) as suggested here:
* https://github.com/platformio/platform-espressif32/issues/1081#issuecomment-1518601054

62910038 - 2023-04-28 - netmindz : Merge pull request #37 from netmindz/mdev Update FX.cpp

d4bdb303 - 2023-04-24 - netmindz : Update FX.cpp Assign proper attribution of DJLight to Stefan Petrick

  fb3477e5 - 2023-04-21 - Frank : soundreactive effect updated 
* blurz: some visual improvements
* Matripix: improved color smoothness, Color by frequency (instead of volume), option to use sound pressure
* pixelwave: improved color selection, use sound energy instead of volume
* freqwave: some speedups, option to show frequency with "musical scale"
* gravfreq: fixed some math accidents that lead to horrible flickering
* default setting improved for some effects

d5a7f5dd - 2023-04-21 - Frank : scrolling text bugfix effect was crashing with too long or undefined segment names.

8e9db0ad - 2023-04-21 - Frank : more accurate FPS forESP32 the standard millis() code is very inaccurate in the "high FPS" ranges. This replaces it with the esp32 high resolution timer.

9130e4be - 2023-04-21 - Frank : minor optimization of core LED functions 
* use _fast_ integer types in loops - in contrast to "uint16_t" etc, the compiler can leave out range/overflow corrections, so it might run faster.
* fcn_declare.h: revive "WLED_USE_REAL_MATH" option, which can be a bit faster on ESP32.

36356743 - 2023-04-21 - Frank : audio effects: allow to run at full speed 
* set the "speed" slider to 255, for running at full speed
* #FPS (framerate) and #POW (ampere) added to scrolling text

00661de7 - 2023-04-21 - Frank : accept up to 250 fps target in LED preferences warning included.

63a597b9 - 2023-04-20 - Frank : pio: same for -S3 ..... 
Tool Manager: toolchain-xtensa-esp32s3@8.4.0+2021r2-patch3 has been installed!
Tool Manager: Installing espressif/toolchain-riscv32-esp @ 8.4.0+2021r2-patch3
Error: Could not find the package with 'espressif/toolchain-riscv32-esp @ 8.4.0+2021r2-patch3' requirements for your system 'linux_x86_64'
Error: Process completed with exit code 1.

b35cd214 - 2023-04-20 - Frank : pio: disable -C3 and -S2 builds until github fixes their build toolds 
Tool Manager: toolchain-xtensa-esp32s2@8.4.0+2021r2-patch3 has been installed!
Tool Manager: Installing espressif/toolchain-riscv32-esp @ 8.4.0+2021r2-patch3
Error: Could not find the package with 'espressif/toolchain-riscv32-esp @ 8.4.0+2021r2-patch3' requirements for your system 'linux_x86_64'

33a78bef - 2023-04-20 - Frank : a little less buffer for -S2 the last change caused a build error for ESP32-S2: region `dram0_0_seg' overflowed by 5064 bytes

1b3d9a1a - 2023-04-20 - Frank : more JSON buffer for boards with PSRAM allows to load ledmaps with > 15000 positions!

bcbc0fbd - 2023-04-19 - Frank : Update platformio.ini 
* temporarily remove esp32c3dev_4MB_M from nightly builds, as the github action build currently has strange problems with it
* -D WLED_USE_PSRAM_JSON for ESP32 boards, as using PSRAM for LED Buffers and Segment Buffers causes slow-down
d90ee766 - 2023-04-19 - Frank : PSRAM: you can have it, and eat it or not eat it *This patch allows to compile with BOARD_HAS_PSRAM, but not set WLED_USE_PSRAM - reserved pins will be protected, and PSRAM usage will be shown in info.
* if you add `-D WLED_USE_PSRAM_JSON` then PSRAM will be used for some JSON buffers, but not for LEDs and Segments.

e2d3800f - 2023-04-19 - Frank : woraround for spurious crash in serializePalettes the root cause of the crash is not really clear, as the problem seems to occur randomly, mosr frequent with fresh installations.
This workaround prevents the array bounds violation, by re-using the last valid  gGradientPalettes entry.

a2f15c77 - 2023-04-19 - Frank : WIFI_POWERON_HACK for AP mode reduce TX power - required for C3 mini v1.0.0 (wemos), see https://www.wemos.cc/en/latest/c3/c3_mini_1_0_0.html#about-wifi

0558865c - 2023-04-18 - Troy : Merge pull request #36 from Fonta/patch-1 Fix invalid environment error in PlatformIO

2e118938 - 2023-04-18 - Troy : Merge pull request #35 from troyhacks/DDP-RGBW-Transmit-Fix DDP Transmit RGBW Fix

8d85a524 - 2023-04-17 - Frank : correct some stupid peak detection defaults parameters C1 and C2 control peak detection. Previous defaults (c2=0 !!!) did not make any sense.

3f429439 - 2023-04-17 - Frank : Blurz effect: back to original SR code 
Modifications from upstream have made the effect kind of boring non-reactive. So we go back to the original effect.
HINT: Effect looks best with _segment_ brightness set to max (use _global_ brightness to reduce brightness as you like).

45da3121 - 2023-04-16 - Fonta : Update platformio.ini 

6b6c961a - 2023-04-16 - Fonta : Fix invalid environment error in PlatformIO PlatformIO gives error on codm environments
``Error: Invalid environment name 'codm-controller-0.6'. The name can contain alphanumeric, underscore, and hyphen characters (a-z, 0-9, -, _)``

28c737df - 2023-04-15 - Frank : small fix Serial0 does not exist without ARDUINO_USB_CDC_ON_BOOT

0fd26cc7 - 2023-04-15 - Frank : replace AC WebServer with lost-hope variant temporarily replace the webserver with a   modified one that can also show .wled and .log files under /edit.

2585b785 - 2023-04-15 - Frank : remove duplictate dependancies  (AsyncTCP 1.1.1) 
* moving "pbolduc/AsyncTCP.git @ 1.2.0" on top of lib_deps, to prevent that AsyncTCP 1.1.1 is pulled in (due due dependacies from Aircoookie/ESPAsyncWebServer
* remove duplicate env.lib_deps from -S2 environments

c295c877 - 2023-04-15 - Frank : moving esp_dmx lib into esp32_4MB_V4_S_base the idea is to keep enable flag and library in the same build env.

244a6137 - 2023-04-15 - Frank : esp32_4MB_V4_M: stay below 100% flash usage 

322ab9c5 - 2023-04-15 - Frank : arti-fx error handling improvements 
- if log file cannot be created, switch to serial logging
- fixing a broken format string
- usermod_arti: avoid to copy more than what fits into the buffer

b7f1373e - 2023-04-14 - TroyHacks : DDP Transmit RGBW Fix 

4294f601 - 2023-04-14 - Frank : npm run build 
cc9a19bc - 2023-04-14 - Frank : partial merge of upstream/main 
* leaving out DotStarHspi5MhzMethod, as we are still on NPB 2.6.9 for eth boards
* leaving out the index.css/index.css changes, as I'm not sure how to merge this.
@ewoudwijma we need to merge the JS and CSS parts when you are back; I'll stay with our MM version for now.

ee23827f - 2023-04-14 - netmindz : Merge pull request #16 from netmindz/audio-palette-updates Audio palette updates

cc25a21b - 2023-04-14 - Will Tatam : Merge branch 'mdev' into audio-palette-updates 

05c3e569 - 2023-04-14 - Frank : optional: warn about functions with high stack usage 

3e2a6848 - 2023-04-14 - Frank : arti  setup(): attempt to fix memory leak 
- check that programName is not too long (fileNameLength-7 is the limit)
- try to fix a memory leak, as programText must be free'd in case of error.
@ewoudwijma please review my changes, I'm not 100% sure I did it right.

10ca7c83 - 2023-04-14 - Frank : enumerateLedmaps: prevent buffer overflow make sure that bounds of char fileName[33] are not exceeded by sprintf.

5f4dd53b - 2023-04-14 - Frank : V4 target: enable warning for variable shadoing 
* pio.ini: add "-Wshadow=compatible-local" for V4 targets
* pio.ini: fix alignment for 8266 build_flags
* fix one (harmless) case of shadowed vars in MM specific code

db62153e - 2023-04-13 - Frank : fix for a potential array overrun unguarded sprintf / strcpy are always a risk.

122f54a2 - 2023-04-13 - Frank : prevent heat-up on tiny -C3 boards 
* reduce LED default brightness
* unset "disable wifi sleep" when WLEDMM_WIFI_POWERON_HACK

94a7f562 - 2023-04-13 - Frank : handling of Serial on CDC USB board ... like the typical -C3
* Replaced a few direct Serial.printf with macros
* Always check if Serial is connected before printing (CDC sometimes hangs  when trying to send/receive without connection)

0081122f - 2023-04-13 - Frank : buildenv improvement for -C3 
* IRremoteESP8266 @ ~2.8.2
* -D WLED_DISABLE_ADALIGHT (as most devices don't have a serial-to-USB chip)

a193aabd - 2023-04-13 - Frank : Merge pull request #34 from troyhacks/2023-04-12-Art-Net_Transmit_Repair_Bad_Optimization 
"Unfixing" an optimization to the Art-Net header.
The local "buffer" was shadowing the LED buffer (function parameter), so art-net would only send out headers but no LEDs.
2e0d1046 - 2023-04-13 - Frank : some cleanups and updates for -C3 * remove duplicate env.lib_deps
* use NeoPixelBus @ 2.7.3
* added board_build.flash_mode

0afad594 - 2023-04-13 - Frank : MM style buildenv for seeedxiao -C3 

40e614cb - 2023-04-13 - Frank : ups double platform_packages line removed

e9719900 - 2023-04-13 - Frank : pio: added esp32.platformV4_new = espressif32 @ ~5.2.0 

0ae004ff - 2023-04-13 - Frank : buildenv fix: avoid NeoPixelBus 2.7.4 it seems that NPB 2.7.4 introduces new incompatibilities with WLED, that break gh action builds.

deb09c28 - 2023-04-13 - TroyHacks : Unmessing an optimization to the header - which caused the header to be sent over and over. 

04fa3995 - 2023-04-11 - Frank : soundsim bugfix FFT_MajorPeak simulated value was too small.

a1bdb47c - 2023-04-10 - Frank : trying to make sound pressure less boring for line-in "sound pressure" for line-in was always close to max - which is expected, because the ADC chip utilize the full 24/16bit sample range.
The new calculation leads to some more "movement".

25122f98 - 2023-04-10 - Frank : temporary disable DMX input on -C3 and -S2 

8ba43b63 - 2023-04-10 - Frank : Sound pressure: modified correction factors for PDM and analog 

61949cfd - 2023-04-10 - Frank : Sound Pressure 
- some optimizations 
- slightly extend input range
- add correction factors for some sound sources
- gravimeter: tweaking

822fcf27 - 2023-04-08 - Ewoud : ARTI-FX change .wled.log to .log 

79c67122 - 2023-04-08 - Will Tatam : Enable WLED_ENABLE_DMX_INPUT again, now we reference a preditacble tag not branch 

eb3ad99b - 2023-04-08 - Will Tatam : Use taged version of esp_dmx 

343252f6 - 2023-04-08 - Will Tatam : Use taged version of esp_dmx 

876b08e3 - 2023-04-08 - Ewoud : Temporary disable WLED_ENABLE_DMX_INPUT in esp32_4MB_V4_S_base 

ca9bd227 - 2023-04-08 - Ewoud : Merge remote-tracking branch 'upstream/main' into mdev Everything merged except platformio.ini
4ld has not been merged previously
Update version to 0.14.0-b15.22

212126b0 - 2023-04-07 - Ewoud : esp8266_4MB_M: usermods maches max usermods, add net print,set flashsize 

a6e2cf0b - 2023-04-07 - Ewoud : ARTI-FX: Fix printing to USER_PRINT (if !logToFile) 

4aea3970 - 2023-04-07 - Ewoud : ARTI-FX support 8266 (experimental!!) add soundpressure Add ARTI-FX to esp8266_4MB_M (experimental!)

20a91454 - 2023-04-06 - Ewoud : Post marge: regenerate html_settings 

6ef2857d - 2023-04-06 - MoonModules : Merge pull request #28 from netmindz/DMX-Input-esp_dmx Dmx input esp dmx

7ffe25d5 - 2023-04-06 - MoonModules : Merge branch 'mdev' into DMX-Input-esp_dmx 

6cce70b2 - 2023-04-06 - Frank : gravimeter and waverly: option to show sound pressure level 
* adjusted gravimeter and waverly effects so that "Sound Pressure" can be used instead of volume
* some improvements to gravimeter effect
* fixing some over/underflows in gravimeter
* waverly: option "No Clouds" to only show lower part

197e120e - 2023-04-06 - Frank : estimated audio sound pressure 

b0907762 - 2023-04-06 - Frank : low-cut audio input filtering 
* 40Hz low-cut and DC blocker filter - will remove any signal offsets and also removes rumbling noise up to 12db
* DC blocker set as default for all sources (prerequisite for later measuring sound pressure)
additional filtering options are in the making :-)

00e9c592 - 2023-04-06 - MoonModules : Update readme.md 

a77900b0 - 2023-04-06 - MoonModules : Update readme.md 

669b81de - 2023-04-06 - MoonModules : Update readme.md 

753f5621 - 2023-04-06 - Ewoud : ws sendLiveLedsWs: no skiplines to show large matrices uncompressed 

7372d304 - 2023-04-05 - MoonModules : Update FUNDING.yml 

64041836 - 2023-04-05 - Ewoud : Merge pull request #30 from troyhacks/ES8388-init-fixes ES8388 init optimizations and fixes

95d6d186 - 2023-04-05 - TroyHacks : ES8388 init optimizations and fixes 

d64cefb2 - 2023-04-05 - Will Tatam : Fix invert of tx and rx pins 

cae1c004 - 2023-04-05 - Ewoud : ARTIFX add support for pixelart + small changes arti_wled.h:

e4243c4d - 2023-04-05 - Ewoud : Merge pull request #5 from netmindz/ES8388 WiP - ES8388

84f316cd - 2023-04-04 - netmindz : Merge pull request #1 from troyhacks/ES8388-troyhacks Working proof of concept for ES8388

111c8c92 - 2023-04-04 - TroyHacks : Merge branch 'ES8388-troyhacks' of https://github.com/troyhacks/WLED into ES8388-troyhacks 

f44f307f - 2023-04-04 - TroyHacks : Comments and typos, init optimization and shortening. 

7d32bc5f - 2023-04-04 - Troy : Merge branch 'ES8388' into ES8388-troyhacks 

a6a1bbab - 2023-04-04 - TroyHacks : Remove platform.ini entry for ES8388 

c38baf90 - 2023-04-04 - TroyHacks : Removing local lib copy 

d775f7fb - 2023-04-04 - TroyHacks : Removed reliance on the ES8388 library and made things more in line with similar boards with I2C init. 

4997145d - 2023-04-04 - Ewoud : Fastled usermod, add Stefan Petrick effects PolarBasics & CircularBlobs CC BY-NC 3.0 licensed effects only include this usermod only if you accept the terms!
Therefore not enabled in platformio.ini builds.

bd477624 - 2023-04-04 - TroyHacks : Working proof of concept for ES8388 

03570848 - 2023-04-03 - Will Tatam : Merge branch 'mdev' into ES8388 

760ff836 - 2023-04-03 - Will Tatam : Merge branch 'mdev' into ES8388 

d17a41f7 - 2023-04-02 - Blaž Kristan : Merge pull request #3155 from werkstrom/patch-1 Adjustments to Pixel Art Converter

503f71f0 - 2023-04-02 - Blaz Kristan : Npm run build 

329899f4 - 2023-04-02 - Ewoud : ooops 

3dd78731 - 2023-04-02 - Ewoud : First b15 daily build: add fastled usermod 

9307105b - 2023-04-02 - Henrik : Redone in Patch-1 

27e89151 - 2023-04-02 - Ewoud : Versioning: 0.14.0-b15 (use the .21 extension on future commits) 

567daf99 - 2023-04-02 - Henrik : Merge branch 'Aircoookie:main' into patch-1 

eead626d - 2023-04-02 - Ewoud : 0.14.0-b15.21 release! 
```
