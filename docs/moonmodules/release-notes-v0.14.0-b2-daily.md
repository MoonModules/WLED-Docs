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
  
git log mdev --pretty=format:"%h - %an, %ad : %s" --date=format-local:"%Y-%m-%d" --since="2023-04-02"
  
c0a0f66a - Frank, 2023-04-30 : trying to revive github ci build for new MCUs (#38)
62910038 - netmindz, 2023-04-28 : Merge pull request #37 from netmindz/mdev
d4bdb303 - netmindz, 2023-04-24 : Update FX.cpp
fb3477e5 - Frank, 2023-04-21 : soundreactive effect updated
d5a7f5dd - Frank, 2023-04-21 : scrolling text bugfix
8e9db0ad - Frank, 2023-04-21 : more accurate FPS forESP32
9130e4be - Frank, 2023-04-21 : minor optimization of core LED functions
36356743 - Frank, 2023-04-21 : audio effects: allow to run at full speed
00661de7 - Frank, 2023-04-21 : accept up to 250 fps target in LED preferences
63a597b9 - Frank, 2023-04-20 : pio: same for -S3 .....
b35cd214 - Frank, 2023-04-20 : pio: disable -C3 and -S2 builds until github fixes their build toolds
33a78bef - Frank, 2023-04-20 : a little less buffer for -S2
1b3d9a1a - Frank, 2023-04-20 : more JSON buffer for boards with PSRAM
bcbc0fbd - Frank, 2023-04-19 : Update platformio.ini
d90ee766 - Frank, 2023-04-19 : PSRAM: you can have it, and eat it or not eat it
e2d3800f - Frank, 2023-04-19 : woraround for spurious crash in serializePalettes
a2f15c77 - Frank, 2023-04-19 : WIFI_POWERON_HACK for AP mode
0558865c - Troy, 2023-04-18 : Merge pull request #36 from Fonta/patch-1
2e118938 - Troy, 2023-04-18 : Merge pull request #35 from troyhacks/DDP-RGBW-Transmit-Fix
8d85a524 - Frank, 2023-04-17 : correct some stupid peak detection defaults
3f429439 - Frank, 2023-04-17 : Blurz effect: back to original SR code
45da3121 - Fonta, 2023-04-16 : Update platformio.ini
6b6c961a - Fonta, 2023-04-16 : Fix invalid environment error in PlatformIO
28c737df - Frank, 2023-04-15 : small fix
0fd26cc7 - Frank, 2023-04-15 : replace AC WebServer with lost-hope variant
2585b785 - Frank, 2023-04-15 : remove duplictate dependancies  (AsyncTCP 1.1.1)
c295c877 - Frank, 2023-04-15 : moving esp_dmx lib into esp32_4MB_V4_S_base
244a6137 - Frank, 2023-04-15 : esp32_4MB_V4_M: stay below 100% flash usage
322ab9c5 - Frank, 2023-04-15 : arti-fx error handling improvements
b7f1373e - TroyHacks, 2023-04-14 : DDP Transmit RGBW Fix
4294f601 - Frank, 2023-04-14 : npm run build
cc9a19bc - Frank, 2023-04-14 : partial merge of upstream/main
ee23827f - netmindz, 2023-04-14 : Merge pull request #16 from netmindz/audio-palette-updates
cc25a21b - Will Tatam, 2023-04-14 : Merge branch 'mdev' into audio-palette-updates
05c3e569 - Frank, 2023-04-14 : optional: warn about functions with high stack usage
3e2a6848 - Frank, 2023-04-14 : arti  setup(): attempt to fix memory leak
10ca7c83 - Frank, 2023-04-14 : enumerateLedmaps: prevent buffer overflow
5f4dd53b - Frank, 2023-04-14 : V4 target: enable warning for variable shadoing
db62153e - Frank, 2023-04-13 : fix for a potential array overrun
122f54a2 - Frank, 2023-04-13 : prevent heat-up on tiny -C3 boards
94a7f562 - Frank, 2023-04-13 : handling of Serial on CDC USB board
0081122f - Frank, 2023-04-13 : buildenv improvement for -C3
a193aabd - Frank, 2023-04-13 : Merge pull request #34 from troyhacks/2023-04-12-Art-Net_Transmit_Repair_Bad_Optimization
2e0d1046 - Frank, 2023-04-13 : some cleanups and updates for -C3
0afad594 - Frank, 2023-04-13 : MM style buildenv for seeedxiao -C3
40e614cb - Frank, 2023-04-13 : ups
e9719900 - Frank, 2023-04-13 : pio: added esp32.platformV4_new = espressif32 @ ~5.2.0
0ae004ff - Frank, 2023-04-13 : buildenv fix: avoid NeoPixelBus 2.7.4
deb09c28 - TroyHacks, 2023-04-13 : Unmessing an optimization to the header - which caused the header to be sent over and over.
04fa3995 - Frank, 2023-04-11 : soundsim bugfix
a1bdb47c - Frank, 2023-04-10 : trying to make sound pressure less boring for line-in
25122f98 - Frank, 2023-04-10 : temporary disable DMX input on -C3 and -S2
8ba43b63 - Frank, 2023-04-10 : Sound pressure: modified correction factors for PDM and analog
61949cfd - Frank, 2023-04-10 : Sound Pressure - some optimizations
822fcf27 - Ewoud, 2023-04-08 : ARTI-FX change .wled.log to .log
79c67122 - Will Tatam, 2023-04-08 : Enable WLED_ENABLE_DMX_INPUT again, now we reference a preditacble tag not branch
eb3ad99b - Will Tatam, 2023-04-08 : Use taged version of esp_dmx
343252f6 - Will Tatam, 2023-04-08 : Use taged version of esp_dmx
876b08e3 - Ewoud, 2023-04-08 : Temporary disable WLED_ENABLE_DMX_INPUT in esp32_4MB_V4_S_base
ca9bd227 - Ewoud, 2023-04-08 : Merge remote-tracking branch 'upstream/main' into mdev
212126b0 - Ewoud, 2023-04-07 : esp8266_4MB_M: usermods maches max usermods, add net print,set flashsize
a6e2cf0b - Ewoud, 2023-04-07 : ARTI-FX: Fix printing to USER_PRINT (if !logToFile)
4aea3970 - Ewoud, 2023-04-07 : ARTI-FX support 8266 (experimental!!) add soundpressure
20a91454 - Ewoud, 2023-04-06 : Post marge: regenerate html_settings
6ef2857d - MoonModules, 2023-04-06 : Merge pull request #28 from netmindz/DMX-Input-esp_dmx
7ffe25d5 - MoonModules, 2023-04-06 : Merge branch 'mdev' into DMX-Input-esp_dmx
6cce70b2 - Frank, 2023-04-06 : gravimeter and waverly: option to show sound pressure level
197e120e - Frank, 2023-04-06 : estimated audio sound pressure
b0907762 - Frank, 2023-04-06 : low-cut audio input filtering
00e9c592 - MoonModules, 2023-04-06 : Update readme.md
a77900b0 - MoonModules, 2023-04-06 : Update readme.md
669b81de - MoonModules, 2023-04-06 : Update readme.md
753f5621 - Ewoud, 2023-04-06 : ws sendLiveLedsWs: no skiplines to show large matrices uncompressed
7372d304 - MoonModules, 2023-04-05 : Update FUNDING.yml
64041836 - Ewoud, 2023-04-05 : Merge pull request #30 from troyhacks/ES8388-init-fixes
95d6d186 - TroyHacks, 2023-04-05 : ES8388 init optimizations and fixes
d64cefb2 - Will Tatam, 2023-04-05 : Fix invert of tx and rx pins
cae1c004 - Ewoud, 2023-04-05 : ARTIFX add support for pixelart + small changes
e4243c4d - Ewoud, 2023-04-05 : Merge pull request #5 from netmindz/ES8388
84f316cd - netmindz, 2023-04-04 : Merge pull request #1 from troyhacks/ES8388-troyhacks
111c8c92 - TroyHacks, 2023-04-04 : Merge branch 'ES8388-troyhacks' of https://github.com/troyhacks/WLED into ES8388-troyhacks
f44f307f - TroyHacks, 2023-04-04 : Comments and typos, init optimization and shortening.
7d32bc5f - Troy, 2023-04-04 : Merge branch 'ES8388' into ES8388-troyhacks
a6a1bbab - TroyHacks, 2023-04-04 : Remove platform.ini entry for ES8388
c38baf90 - TroyHacks, 2023-04-04 : Removing local lib copy
d775f7fb - TroyHacks, 2023-04-04 : Removed reliance on the ES8388 library and made things more in line with similar boards with I2C init.
4997145d - Ewoud, 2023-04-04 : Fastled usermod, add Stefan Petrick effects PolarBasics & CircularBlobs
bd477624 - TroyHacks, 2023-04-04 : Working proof of concept for ES8388
03570848 - Will Tatam, 2023-04-03 : Merge branch 'mdev' into ES8388
760ff836 - Will Tatam, 2023-04-03 : Merge branch 'mdev' into ES8388
d17a41f7 - Blaž Kristan, 2023-04-02 : Merge pull request #3155 from werkstrom/patch-1
503f71f0 - Blaz Kristan, 2023-04-02 : Npm run build
329899f4 - Ewoud, 2023-04-02 : ooops
3dd78731 - Ewoud, 2023-04-02 : First b15 daily build: add fastled usermod
9307105b - Henrik, 2023-04-02 : Redone in Patch-1
27e89151 - Ewoud, 2023-04-02 : Versioning: 0.14.0-b15 (use the .21 extension on future commits)
567daf99 - Henrik, 2023-04-02 : Merge branch 'Aircoookie:main' into patch-1
eead626d - Ewoud, 2023-04-02 : 0.14.0-b15.21 release!
