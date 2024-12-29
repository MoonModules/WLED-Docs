---
title: HUB75 support
---

WLED-MM now features support for LED matrix panels using the HUB75 format

You can use either a regular ESP32 with a suitable adapter board such as [ESP32 Trinity](https://esp32trinity.com/) or [rorosaurus/esp32-hub75-driver](https://github.com/rorosaurus/esp32-hub75-driver) or the dedicated [Adafruit Matrix Portal S3](https://www.adafruit.com/product/5778)

This support is supplied by the [ESP32-HUB75-MatrixPanel-DMA](https://github.com/mrcodetastic/ESP32-HUB75-MatrixPanel-DMA?tab=readme-ov-file) library, so see here for more details about supported hardware

Support for HUB75 in WLED-MM should be considered experimental at the moment, but we welcome early feedback on this new feature - please share your experience in the [2D channel](https://discord.gg/Pgdv8MgR)

# Setup
## Required Software Build
### Adafruit Matrix Portal S3
Please use the dedicated adafruit_matrixportal_esp32s3 build as this is pre-configured for the pins needed for HUB75 output

### Huidu HD-WF2 ESP32-S3
* Hold the button down as you use a USB-A to USB-A cable to upload esp32S3_4MB_S
* See more at https://github.com/mrcodetastic/ESP32-HUB75-MatrixPanel-DMA/issues/433

### Generic ESP32 support
You must use a build with WLED_ENABLE_HUB75MATRIX defined, for example, esp32_4MB_V4_S. If you do not see Hub75 options in the list of LED types, you are not using the correct build

If you are using a board such as the ESP32 Trinity or other boards wired for the default pinout of the ESP32-HUB75-MatrixPanel-DMA driver, this is selected by default

![display_esp32_wiring_bb](https://github.com/user-attachments/assets/9fd3cf9f-b6b3-42ce-ba52-cea015e95024)


If you are using the rorosaurus/esp32-hub75-driver or any other board using the SmartMatrix default pinout then you will need to do a custom build with ESP32_FORUM_PINOUT defined

If you are using any other config, you currently need to edit wled00/bus_manager.cpp to add a new elif block and define to your build - it is not possible to set the HUB75 pin config in LED preferences at the moment

## Configuration
### Panel size and chain length
* Due to limitations in the HUB75 DMA driver, only these panel dimensions are supported:
  * 32 x 32 (2-scan or 4-scan)
  * 64 x 32 (2-scan or 4-scan)
  * 64 x 64 (2-scan or 4-scan)
  * 128 x 64 (2-scan or 4-scan).
* Only _one HUB75e port_ is supported.
* Please chain your panels (panel#1 _OUT_ --> panel#2 _IN_) if you want to control more than one panel.
* Maximum possible size:
  * Classic ESP32: the maximum possible size is 128x64 - however WLEDMM might get unstable with this setup. We recommend to use no more than 64x64 on classic esp32.
  * ESP32-S3 without PSRAM (including Huidu HD-WF2): the maximum possible size is 128x64, however we recommend to use 64x64 because the firmware might get unstable above this size.
  * ESP32-S3 with PSRAM - octal "opi" PSRAM recommended (including LilyGO T7-S3) : the maximum possible size is 256x64, i.e. 4 chained panels of 64x64 pixels each.
  * ESP32-S2 is possible, however _not recommended_ due to smaller RAM
  * ESP32-C3, ESP32-C6 and ESP8266 do not support HUB75

### Setup
First, you must set the LED output to match the correct Hub75Matrix option for the panel size you are using. The chain length is the number of panels connected. Note: currently only a horizontal chain of panels is supported. ~~You can used 2D setup to configure physical panel positions~~ unfortunately it's not possible to use 2D setup to change the panel layout of chained panels.

Next, you need to go into the 2D Configuration and create a _single_ matrix with the total size of your hub75 setup. e.g a chain of 2 panels with 32x32 pixels each, would be created as a 64x32 matrix in the 2D configuration page


## HUB75 Known Problems and Limitations 
* Maximum possible sizes: see previous section
* Currently only a horizontal chain of panels is supported through the WLED settings, for other layouts you need to edit the source. See [Virtual Matrix Panel](https://github.com/mrcodetastic/ESP32-HUB75-MatrixPanel-DMA/blob/master/examples%2FVirtualMatrixPanel%2FREADME.md) for more info 
* combining HUB75 with other LED types (including virtual leds) was not tested yet - it may or may not work.
* classic ESP32: using audioreactive microphones (or line-in) causes crashes and wifi instabilities. You can still use UDP sound receive for receiving audio data from another board. Please select "None - network receive only" as DigitalMic type.
* ESP32-S2: its not possible to use HUB75 and audioreactive at the same time.
* ESP32-S3: After changing HUB75 options (LED preferences), your display will go black. You need to reboot for driver changes to take effect.
