---
title: Release notes v0.14.0-b2-daily
hide:
  # - navigation
  # - toc
---

Below are the ongoing updates in WLEDMM which has not made it to a release yet (Next release will be v0.14.0-b2)

## Support for pixelArt in ARTI-FX
5 April 2023

<video width="400" autoplay><source src="https://user-images.githubusercontent.com/1737159/230075460-6652b18e-23ab-4138-a49c-e919b0bcb639.mov" type="video/mp4"></video>

Program can be found here: https://github.com/MoonModules/WLED-Effects/blob/master/ARTIFX/wled/mario.wled

<img width="314" alt="Screenshot 2023-04-05 at 13 33 28" src="https://user-images.githubusercontent.com/1737159/230075763-6186f8bd-e915-4f63-a7bb-6ea9e3dd2249.png">

As ARTIFX does not support strings, jsonToPixels only contains a sequence number, the name of the json files is combination of segment name (that should be called mario), sequence number and ".json")
See https://github.com/MoonModules/WLED-Effects/blob/master/ARTIFX/wled/presets.json for how to add mario in presets 

And don't forget to upload latest wledv033.json to <ip>/edit (https://github.com/MoonModules/WLED-Effects/blob/master/ARTIFX/wled/wledv033.json)

## Add ES8388 as Sound Reactive Input type
5 April 2023
By @Troy and @Netmindz

<img width="164" alt="Screenshot 2023-04-05 at 12 06 27" src="https://user-images.githubusercontent.com/1737159/230072580-16ed4113-6c54-443f-a848-4cbf745cc682.png">

Can be found in these boards:

<img width="243" src="https://user-images.githubusercontent.com/1737159/230074117-97d75509-5511-47d2-a0c5-87ad622085c1.jpeg">

[LyraT v4.3](https://espressif-docs.readthedocs-hosted.com/projects/esp-adf/en/latest/design-guide/dev-boards/board-esp32-lyrat-v4.3.html)

<img width="243" src="https://user-images.githubusercontent.com/1737159/230074148-a88e43d5-2218-4f6c-811a-dc092608a8e2.jpeg">
(?)
