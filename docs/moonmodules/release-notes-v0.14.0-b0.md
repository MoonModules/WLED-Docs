---
title: Release notes v0.14.0-b0
hide:
  # - navigation
  # - toc
---

## Adding pong
September 16, 2022

### Adding pong
In games usermod

<video width="248" autoplay><source src="https://user-images.githubusercontent.com/1737159/192528357-3cda343c-de1c-4820-adb6-fb71fdfdd1f2.mov" type="video/mp4"></video>

## updates from audio-reactive
September 8, 2022

### updates from audio-reactive
#### merged to upstream
* volume & frequency "dynamics limiter" - slower decay of sound volume in effects. Also has an effect on GEQ, as it turns on smoothing for frequency bands. 
<img width="400" alt="image" src="https://user-images.githubusercontent.com/91616163/189164956-9f5cf51c-d725-4691-94d3-8ab60d8e384c.png">

* GEQ frequency scaling: None (as in SR WLED), Linear, Square Root (new default), Logarithmic. 
<img width="450" alt="image" src="https://user-images.githubusercontent.com/91616163/189165448-61d4c080-2501-42fc-b975-da87bc2adfe9.png">

#### work in progress
* New option "MIC profile" - default (same table as in SR WLED), line-in (strictly "pink noise"), IMNP441 (optimized), ICS-43434 (optimized). 
This option causes the use of different "pink noise tables" when adjusting the frequency spectrum to human "hearing sensitivity". Pink noise calibration is very common when using hardware Equalizers. A good testcase is this [Pink Noise Video](https://www.youtube.com/watch?v=noapz4XPR6g).
<img width="400" alt="image" src="https://user-images.githubusercontent.com/91616163/189166244-482f4530-7d18-42af-ac4f-27bd0bfe5f95.png">

* (minor) Showing the "GEQ input gain" in percent, next to the slider value. 
![image](https://user-images.githubusercontent.com/91616163/189167784-ea972e67-cac0-4b7c-85de-fc024291ddb0.png)

* user-settable "Trebble Amplification" for GEQ effects. Will be placed into the Info Page, directly under "GEQ input gain".


## FrameWork-V4
September 6

**Lessons Learnt**: When upgrading WLED devices to software using the IDF 4.4.x framework, it seems that a flash erase is needed. Without this, we observed crashes whenever files were written.

Suspected cause: Lorol LittleFS (from standards framework) is not compatible with the built-in littleFS from IDF v4.4 / arduino-esp32 v2.0.4. Could be that the partition table is the problem, so a chip erase is needed to clean the table.

A new merge to mdev has been done: new environment `esp32mdev_V4` so that normal compiles are not getting the new framework automatically.


### updates from audioreactive-prototype
* Will merge into upstream

### Json Mapping
From excel/vba <img width="181" alt="image" src="https://user-images.githubusercontent.com/1737159/188688306-b5a5e7d8-3172-43b8-9f53-778ff9a2df3b.png"> via /edit and <img width="98" alt="image" src="https://user-images.githubusercontent.com/1737159/188688993-34c73f35-b642-4120-b31d-c87ea58ea10e.png">
 to matrix <img width="160" alt="image" src="https://user-images.githubusercontent.com/1737159/188688601-73a9e7f8-34d9-463f-9ec3-1cacaea13d6b.png">

Files are here: [JSONMappings](https://github.com/MoonModules/WLED-Effects/tree/master/JSONMappings)

## September 2
### updates from audioreactive-prototype
Merged into upstream
### Expand1D effects
* Virtual strips in 1D effects

Strip bar has been merged to upstream, strip Arc and strip Corner (as opposed to pixel Arc and Corner, see upstream) is "waiting" in upstream branch. To be added to MoonModules.

<video width="429" autoplay><source src="https://user-images.githubusercontent.com/1737159/192609697-15cc43f8-157e-4a0e-8ea7-32e755bf79ef.mov" type="video/mp4"></video>

### Usermod level up

each usermod <img width="166" alt="image" src="https://user-images.githubusercontent.com/1737159/188707291-c9d55626-6b01-4d28-9d61-0f9adb7eb8d3.png"> got its own settings page <img width="186" alt="image" src="https://user-images.githubusercontent.com/1737159/188712805-bb6bdff5-e762-4031-94ae-46d6e961436a.png">


## September 1

## August 31
### ARTI-FX

<img width="296" alt="image" src="https://user-images.githubusercontent.com/1737159/188725863-3c133079-f6a5-4885-82d8-d603f3c95f3e.png"> + 
<img width="210" alt="image" src="https://user-images.githubusercontent.com/1737159/188725973-0d3ad535-bb9f-459c-848d-8b11f80bd3cc.png"> = 
<img width="216" alt="image" src="https://user-images.githubusercontent.com/1737159/188726087-98f600b3-5f95-432a-854d-f1ff51426ec0.png">

* drawArc using x2+y2=r2 instead of sin/cos

### Weather usermod

<img width="181" alt="image" src="https://user-images.githubusercontent.com/1737159/189068765-e80c8a0e-3e83-44a6-ae1f-4242ee6514da.png"> + 
<img width="234" alt="image" src="https://user-images.githubusercontent.com/1737159/189068898-eb424d9e-b929-4cd9-9e01-2fbc93847e2d.png"> = <img width="216" alt="image" src="https://user-images.githubusercontent.com/1737159/188919809-1dc14eda-90f9-43fc-a7fa-58957dd810c5.png">

## August 29
### updates from audioreactive-prototype

<img width="245" alt="image" src="https://user-images.githubusercontent.com/1737159/188707602-bbf02069-a09d-4c37-884e-785f500958c4.png"><br>
<img width="334" alt="image" src="https://user-images.githubusercontent.com/1737159/188814448-7e74dacc-3bd3-4348-b280-a2cce294b3ff.png">

## Merged into upstream
* Sound simulations
* Expand 1D into 2D
* Virtual strips in 1D effects
* liveview / peek 2D
* AR: reduce variables 
* AR: Sound info in info panel
* Replace leds[] by sPC/gPC
* Slower fade-out in GEQ and a few other audioreactive effects.
* Audio reactive stuff:
* * upgrade to latest ArduinoFFT, using 'float' instead of 'double'. Up to 8 times faster!
* * configurable sound dynamics limiter, to make audioreactive effects flow with the  music, and prevent "sudden flashes at onsets". A kind of 'flicker fixer'.
* * improvements for UDP sound sync
* * new frequency scaling options 'square root' and 'logarithmic' - GEQ shows more action in higher frequencies.
