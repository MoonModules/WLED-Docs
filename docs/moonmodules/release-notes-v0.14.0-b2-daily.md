---
title: Release notes v0.14.0-b2-daily
hide:
  # - navigation
  # - toc
---

Below are the ongoing updates in WLEDMM which has not made it to a release yet (Next release will be v0.14.0-b2)

## SoundPressure
7 April 2023

By @Softhack007

Also supported by ARTI-FX

More info follows

## Audio Palette Updates

14 April 2023

By @Netmindz

Fix issues with Audio Responsive Hue being single color and add new Audio Responsive Ramp palette. AR Ramp is designed for use with effects like Fire that expect the palette to start with black, then ramp up

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

