---
title: Release notes v0.14.0-b2-daily
hide:
  # - navigation
  # - toc
---

Below are the ongoing updates in WLEDMM which has not made it to a release yet (Next release will be v0.14.0-b2)

## Audio Palette Updates

14 April 2023

By @Netmindz

Fix issues with Audio Responsive Hue being single color and add new Audio Responsive Ramp palette. AR Ramp is designed for use with effects like Fire that expect the palette to start with black, then ramp up

## SoundPressure
7 April 2023

By @Softhack007

Also supported by ARTI-FX

More info follows

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
  
git log mdev --pretty=format:"%h - %ad - %an : %s" --date=format-local:"%Y-%m-%d" --since="2023-04-02"

```
c0a0f66a - 2023-04-30 - Frank : trying to revive github ci build for new MCUs (#38)
62910038 - 2023-04-28 - netmindz : Merge pull request #37 from netmindz/mdev
d4bdb303 - 2023-04-24 - netmindz : Update FX.cpp
fb3477e5 - 2023-04-21 - Frank : soundreactive effect updated
d5a7f5dd - 2023-04-21 - Frank : scrolling text bugfix
8e9db0ad - 2023-04-21 - Frank : more accurate FPS forESP32
9130e4be - 2023-04-21 - Frank : minor optimization of core LED functions
36356743 - 2023-04-21 - Frank : audio effects: allow to run at full speed
00661de7 - 2023-04-21 - Frank : accept up to 250 fps target in LED preferences
63a597b9 - 2023-04-20 - Frank : pio: same for -S3 .....
b35cd214 - 2023-04-20 - Frank : pio: disable -C3 and -S2 builds until github fixes their build toolds
33a78bef - 2023-04-20 - Frank : a little less buffer for -S2
1b3d9a1a - 2023-04-20 - Frank : more JSON buffer for boards with PSRAM
bcbc0fbd - 2023-04-19 - Frank : Update platformio.ini
d90ee766 - 2023-04-19 - Frank : PSRAM: you can have it, and eat it or not eat it
e2d3800f - 2023-04-19 - Frank : woraround for spurious crash in serializePalettes
a2f15c77 - 2023-04-19 - Frank : WIFI_POWERON_HACK for AP mode
0558865c - 2023-04-18 - Troy : Merge pull request #36 from Fonta/patch-1
2e118938 - 2023-04-18 - Troy : Merge pull request #35 from troyhacks/DDP-RGBW-Transmit-Fix
8d85a524 - 2023-04-17 - Frank : correct some stupid peak detection defaults
3f429439 - 2023-04-17 - Frank : Blurz effect: back to original SR code
45da3121 - 2023-04-16 - Fonta : Update platformio.ini
6b6c961a - 2023-04-16 - Fonta : Fix invalid environment error in PlatformIO
28c737df - 2023-04-15 - Frank : small fix
0fd26cc7 - 2023-04-15 - Frank : replace AC WebServer with lost-hope variant
2585b785 - 2023-04-15 - Frank : remove duplictate dependancies  (AsyncTCP 1.1.1)
c295c877 - 2023-04-15 - Frank : moving esp_dmx lib into esp32_4MB_V4_S_base
244a6137 - 2023-04-15 - Frank : esp32_4MB_V4_M: stay below 100% flash usage
322ab9c5 - 2023-04-15 - Frank : arti-fx error handling improvements
b7f1373e - 2023-04-14 - TroyHacks : DDP Transmit RGBW Fix
4294f601 - 2023-04-14 - Frank : npm run build
cc9a19bc - 2023-04-14 - Frank : partial merge of upstream/main
ee23827f - 2023-04-14 - netmindz : Merge pull request #16 from netmindz/audio-palette-updates
cc25a21b - 2023-04-14 - Will Tatam : Merge branch 'mdev' into audio-palette-updates
05c3e569 - 2023-04-14 - Frank : optional: warn about functions with high stack usage
3e2a6848 - 2023-04-14 - Frank : arti  setup(): attempt to fix memory leak
10ca7c83 - 2023-04-14 - Frank : enumerateLedmaps: prevent buffer overflow
5f4dd53b - 2023-04-14 - Frank : V4 target: enable warning for variable shadoing
db62153e - 2023-04-13 - Frank : fix for a potential array overrun
122f54a2 - 2023-04-13 - Frank : prevent heat-up on tiny -C3 boards
94a7f562 - 2023-04-13 - Frank : handling of Serial on CDC USB board
0081122f - 2023-04-13 - Frank : buildenv improvement for -C3
a193aabd - 2023-04-13 - Frank : Merge pull request #34 from troyhacks/2023-04-12-Art-Net_Transmit_Repair_Bad_Optimization
2e0d1046 - 2023-04-13 - Frank : some cleanups and updates for -C3
0afad594 - 2023-04-13 - Frank : MM style buildenv for seeedxiao -C3
40e614cb - 2023-04-13 - Frank : ups
e9719900 - 2023-04-13 - Frank : pio: added esp32.platformV4_new = espressif32 @ ~5.2.0
0ae004ff - 2023-04-13 - Frank : buildenv fix: avoid NeoPixelBus 2.7.4
deb09c28 - 2023-04-13 - TroyHacks : Unmessing an optimization to the header - which caused the header to be sent over and over.
04fa3995 - 2023-04-11 - Frank : soundsim bugfix
a1bdb47c - 2023-04-10 - Frank : trying to make sound pressure less boring for line-in
25122f98 - 2023-04-10 - Frank : temporary disable DMX input on -C3 and -S2
8ba43b63 - 2023-04-10 - Frank : Sound pressure: modified correction factors for PDM and analog
61949cfd - 2023-04-10 - Frank : Sound Pressure - some optimizations
822fcf27 - 2023-04-08 - Ewoud : ARTI-FX change .wled.log to .log
79c67122 - 2023-04-08 - Will Tatam : Enable WLED_ENABLE_DMX_INPUT again, now we reference a preditacble tag not branch
eb3ad99b - 2023-04-08 - Will Tatam : Use taged version of esp_dmx
343252f6 - 2023-04-08 - Will Tatam : Use taged version of esp_dmx
876b08e3 - 2023-04-08 - Ewoud : Temporary disable WLED_ENABLE_DMX_INPUT in esp32_4MB_V4_S_base
ca9bd227 - 2023-04-08 - Ewoud : Merge remote-tracking branch 'upstream/main' into mdev
212126b0 - 2023-04-07 - Ewoud : esp8266_4MB_M: usermods maches max usermods, add net print,set flashsize
a6e2cf0b - 2023-04-07 - Ewoud : ARTI-FX: Fix printing to USER_PRINT (if !logToFile)
4aea3970 - 2023-04-07 - Ewoud : ARTI-FX support 8266 (experimental!!) add soundpressure
20a91454 - 2023-04-06 - Ewoud : Post marge: regenerate html_settings
6ef2857d - 2023-04-06 - MoonModules : Merge pull request #28 from netmindz/DMX-Input-esp_dmx
7ffe25d5 - 2023-04-06 - MoonModules : Merge branch 'mdev' into DMX-Input-esp_dmx
6cce70b2 - 2023-04-06 - Frank : gravimeter and waverly: option to show sound pressure level
197e120e - 2023-04-06 - Frank : estimated audio sound pressure
b0907762 - 2023-04-06 - Frank : low-cut audio input filtering
00e9c592 - 2023-04-06 - MoonModules : Update readme.md
a77900b0 - 2023-04-06 - MoonModules : Update readme.md
669b81de - 2023-04-06 - MoonModules : Update readme.md
753f5621 - 2023-04-06 - Ewoud : ws sendLiveLedsWs: no skiplines to show large matrices uncompressed
7372d304 - 2023-04-05 - MoonModules : Update FUNDING.yml
64041836 - 2023-04-05 - Ewoud : Merge pull request #30 from troyhacks/ES8388-init-fixes
95d6d186 - 2023-04-05 - TroyHacks : ES8388 init optimizations and fixes
d64cefb2 - 2023-04-05 - Will Tatam : Fix invert of tx and rx pins
cae1c004 - 2023-04-05 - Ewoud : ARTIFX add support for pixelart + small changes
e4243c4d - 2023-04-05 - Ewoud : Merge pull request #5 from netmindz/ES8388
84f316cd - 2023-04-04 - netmindz : Merge pull request #1 from troyhacks/ES8388-troyhacks
111c8c92 - 2023-04-04 - TroyHacks : Merge branch 'ES8388-troyhacks' of https://github.com/troyhacks/WLED into ES8388-troyhacks
f44f307f - 2023-04-04 - TroyHacks : Comments and typos, init optimization and shortening.
7d32bc5f - 2023-04-04 - Troy : Merge branch 'ES8388' into ES8388-troyhacks
a6a1bbab - 2023-04-04 - TroyHacks : Remove platform.ini entry for ES8388
c38baf90 - 2023-04-04 - TroyHacks : Removing local lib copy
d775f7fb - 2023-04-04 - TroyHacks : Removed reliance on the ES8388 library and made things more in line with similar boards with I2C init.
4997145d - 2023-04-04 - Ewoud : Fastled usermod, add Stefan Petrick effects PolarBasics & CircularBlobs
bd477624 - 2023-04-04 - TroyHacks : Working proof of concept for ES8388
03570848 - 2023-04-03 - Will Tatam : Merge branch 'mdev' into ES8388
760ff836 - 2023-04-03 - Will Tatam : Merge branch 'mdev' into ES8388
d17a41f7 - 2023-04-02 - Blaž Kristan : Merge pull request #3155 from werkstrom/patch-1
503f71f0 - 2023-04-02 - Blaz Kristan : Npm run build
329899f4 - 2023-04-02 - Ewoud : ooops
3dd78731 - 2023-04-02 - Ewoud : First b15 daily build: add fastled usermod
9307105b - 2023-04-02 - Henrik : Redone in Patch-1
27e89151 - 2023-04-02 - Ewoud : Versioning: 0.14.0-b15 (use the .21 extension on future commits)
567daf99 - 2023-04-02 - Henrik : Merge branch 'Aircoookie:main' into patch-1
eead626d - 2023-04-02 - Ewoud : 0.14.0-b15.21 release!
```
