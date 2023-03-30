---
title: Release notes v0.14.0-b1
hide:
  # - navigation
  # - toc
---

## Drop downs for pin variables
December 23, 2022

<img width="150" alt="image" src="https://user-images.githubusercontent.com/1737159/209367375-48841ac7-abc5-4f3f-ab43-16d7cdfb3a06.png">

* show pins which are in use (not selectable)
* excludes pins which may not be used (e.g. for 4ld/mclk variable)
* use global pins option
* undefined option

Currently implemented for AudioReactive and 4LineDisplay (tested) and all usermods which uses pin variables (testing in progress)

## mm.kno.wled.ge
December 21, 2022

[MoonModules pages](https://github.com/MoonModules/WLED-Docs) (wich is a fork of upstream pages) is now linked to [mm.kno.wled.ge](https://mm.kno.wled.ge) and is integrated in MoonModules WLED.

## Usermod specific help
December 19, 2022

<img width="282" alt="image" src="https://user-images.githubusercontent.com/91013628/208895794-27d9920e-2316-4c98-b21a-3319954985ce.png">

This goes to <https://mm.kno.wled.ge/soundreactive/Sound-Settings/>

Also added in Weather usermod and four line display usermod (pages wip)

## Ledmap2D
December 5, 2022
In 0.14 ledmaps are only supported for 1D.
This fix makes it work for 2D in WLED MM.

## ARTI-FX improvements
November 29, 2022

ARTI-FX improvements:
- Simplified [presets.json](https://github.com/MoonModules/WLED-Effects/tree/master/ARTIFX/wled) (can be downloaded directly into WLED MM in ARTI-FX editor screen)
- some bug fixes to let ARTI-FX run better on 2D

And combining ARTI-FX with [1D expansions](#october-21-2022) gives great results and makes ARTI-FX very well performing on large 2D matrices!!!

This is color_fade_pulse (by @atuline) with Circles expansion:

<video width="160" autoplay><source src="https://user-images.githubusercontent.com/1737159/204777643-a93413a8-b430-4499-a9b9-64acd55a351c.mp4" type="video/mp4"></video>

## Improved lay-out usermod settings
November 20, 2022

Grouping and pre-post texts in usermod settings (to make it more readable)

<img width="160" alt="image" src="https://user-images.githubusercontent.com/1737159/202906302-6b4411c8-7aee-4c12-a88c-0f1828232199.png">

## Audioreactive palettes
November 19, 2022

by NetMindz

<img width="296" alt="image" src="https://user-images.githubusercontent.com/1737159/202859807-b33ad565-ddf1-450e-9f0b-27d54b5dd0d8.png">

<video width="296" autoplay><source src="https://user-images.githubusercontent.com/1737159/202907087-6b25d88f-f43f-4d6d-9c39-21a7e9f4a5db.mov" type="video/mp4"></video>

## Extended mic settings in platformIO
November 18, 2022

<img width="692" alt="image" src="https://user-images.githubusercontent.com/1737159/202859001-665f245c-df4e-4c83-83d5-99d79cdc5801.png">

allowing to create mic specific environments:

<img width="261" alt="image" src="https://user-images.githubusercontent.com/1737159/202859113-bb4139a2-ba0a-48ab-bf7a-2d9aa033d3aa.png">

## Bin Aware Builds
October 28, 2022

Upload hardware specific configs based on generated filenames (=> WLED install is aware of underlying hardware).

Ultimate goal of bin awareness is that WLED itself says: hey! I found a new update for you, do you want to install?

<img width="334" alt="image" src="https://user-images.githubusercontent.com/1737159/199474001-0fc84cab-e34f-4236-8d37-1b7cee34e2ce.png">

plus

<img width="657" alt="image" src="https://user-images.githubusercontent.com/1737159/199474203-b9802184-532e-40b6-949e-8aa8f2b0d529.png">

(esp32mdev -> esp32_4MB_min. esp32mdevmax -> esp32_4MB_max / esp32_16MB_max)

plus

<img width="234" alt="image" src="https://user-images.githubusercontent.com/91013628/200820664-90f75ba9-523c-485e-bea3-5abd9713c33b.png">

(0.14.0. sequence of upstream commit . sequence of mm commit (need to be updated together with build date)

=>

<img width="422" alt="image" src="https://user-images.githubusercontent.com/91013628/200820550-abe14707-1f10-4c25-b20a-aa4a3770bfab.png">

=>

<img width="430" alt="image" src="https://user-images.githubusercontent.com/91013628/200820950-6d7be54f-c5fd-4b6a-97c0-6829c3201a13.png">

(WLED install is aware of the filename of it's bin, WLEDMM_0.14.0.2.1_esp32_16MB.bin in this example)

plus

<img width="400" alt="image" src="https://user-images.githubusercontent.com/91013628/200821356-36e51551-b055-493e-a3e4-8b332cad3eb2.png">

(Serg and Wladi repo's should use the same names)

## OTA latest release
October 25, 2022

Manual OTA Update is showing the latest MoonModules/WLED release and clicking on the version icon jumps to the [release pages on Github](https://github.com/MoonModules/WLED/releases), links to Serg74 and Wladi builds are also shown on the release page, so Manual OTA Update will guide you to the version you need!

<img width="398" alt="image" src="https://user-images.githubusercontent.com/91013628/197806516-90f49798-66b7-4989-ae11-590446c19a4a.png">

## Add Circles and Block as 1D expansion 
October 21, 2022

Add Circles and Block as 1D expansion and show virtualStrip effects with ⋮⋮

<img width="642" alt="Screenshot 2022-10-21 at 12 08 29" src="https://user-images.githubusercontent.com/91013628/197171416-266b1727-27cc-497c-b1f6-6953538d9dfc.png">

Tetris effect with block expansion:

<video width="437" autoplay><source src="https://user-images.githubusercontent.com/91013628/197814095-829ebffa-0e56-40af-a2fb-6d58c772a559.mov" type="video/mp4"></video>

## compatibility for SR/0.13 presets
October 20, 2022

Thanks to '_renumbered effect ID's back to WLED SR 0.13 numbering_': Add compatibility for SR/0.13 presets. This allows HB effects to be run on 0.14, however this shows that there are some shortcomings in 0.14: e.g. lissajoux not working as at should and overlapping segments not working (e.g. [Akemi from Hell](https://streamable.com/lze6gl)): November update: Lissajoux, Akemi from Hell (and others) fixed, overlapping segments working now. Check this in Led Preferences:

<img width="452" alt="image" src="https://user-images.githubusercontent.com/1737159/202910638-2c40e2dc-1277-4bf0-ad5b-9a6e97121649.png">

(To see them fully working: load them into WLEDSR 0.13!)

<video width="437" autoplay><source src="https://user-images.githubusercontent.com/91013628/196901131-a10f580c-2637-4c82-8054-abb5b8de4458.mov" type="video/mp4"></video>

To upload HR effects put effects / presets.json in <your wled ip>/edit

To start creating your own multiple segment effects put base / presets.json in <your wled ip>/edit

Presets.json files are [here](https://github.com/MoonModules/WLED-Effects/tree/master/Presets/HB_PresetPack210808_32x32_16seg)

## renumbered effect ID's back to WLED SR 0.13 numbering
October 16, 2022

  **Important update: renumbered effect ID's back to WLED SR 0.13 numbering** so WLED (SR) 0.13 is compatible with MoonModules 0.14 for presets and sync between devices 

<img width="437" alt="image" src="https://user-images.githubusercontent.com/91013628/196028158-c7ab7e2f-8a1c-4c5d-a253-19b11bfe1b6e.png">

## Extra hardware info on Info tab
October 13, 2022

<img width="462" alt="image" src="https://user-images.githubusercontent.com/91013628/196035364-3c38bfc5-f366-4d41-8a3b-56dc8858019d.png">


## Refactored JSON Mapping
October 1, 2022
  
smaller memory footprint so larger mappings can be used, e.g. Snake32:

<video width="405" autoplay><source src="https://user-images.githubusercontent.com/91013628/193404268-fb1cccf2-56af-4045-b654-be84d5ef3c8c.mov" type="video/mp4"></video>

Files are here: [JSONMappings](https://github.com/MoonModules/WLED-Effects/tree/master/JSONMappings)

## Games usermod additions 
September 27, 2022

Added to games usermod:

### 3D to 2D mapping
Adding Frame3D class which takes a 3D coordinate and maps this to 2D matrix (using addEffect(), setPixelColor(floats) and drawLine() added in 0.14 version)

<img width="405" alt="image" src="https://user-images.githubusercontent.com/1737159/192524364-4e870d79-4caa-41ad-ac39-288d71543916.png">    =    <img width="248" alt="image" src="https://user-images.githubusercontent.com/1737159/192523682-3d8cd32d-c589-4fe2-b27e-aecb1d5fbbb0.png">

### 3D + Gyro
Refactoring USERMOD_MPU6050_IMU (so that it works!) using latest ElectronicCats/mpu6050 library
Embedding this usermod in games usermod and use yaw pitch and roll in Frame3D class

<img width="248" alt="image" src="https://user-images.githubusercontent.com/1737159/192523682-3d8cd32d-c589-4fe2-b27e-aecb1d5fbbb0.png">    +    <img width="248" alt="image" src="https://user-images.githubusercontent.com/1737159/192525144-8d8590bf-449f-4336-975e-fced3ea34830.png">    =     <video width="248"autoplay><source src="https://user-images.githubusercontent.com/1737159/192526130-64ba2903-4481-42af-a297-4f18b78ed460.mov" type="video/mp4"></video>

