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
Please use the dedicated adafruit_matrixportal_esp32s3 build as this is pre-configured for HUB75 output

### Huidu HD-WF2 ESP32-S3
* Hold the button down as you use a USB-A to USB-A cable to upload esp32S3_4MB_S
* See more at https://github.com/mrcodetastic/ESP32-HUB75-MatrixPanel-DMA/issues/433

### Generic ESP32 support
You must use a build with WLED_ENABLE_HUB75MATRIX defined, for example, esp32_4MB_V4_S. If you do not see Hub75 options in the list of LED types, you are not using the correct build

If you are using a board such as the ESP32 Trinity or other boards wired for the default pinout of the ESP32-HUB75-MatrixPanel-DMA driver, this is selected by default

![display_esp32_wiring_bb](https://github.com/user-attachments/assets/9fd3cf9f-b6b3-42ce-ba52-cea015e95024)


If you are using the rorosaurus/esp32-hub75-driver or any other board using the SmartMatrix default pinout then you will need to do a custom build with ESP32_FORUM_PINOUT defined

If you are using any other config, you currently need to edit wled00/bus_manager.cpp to add a new elif block and define to your build - it is not possible to set the pin config in LED preferences at the moment

## Configuration
First, you must set the LED output to match the correct Hub75Matrix option for the panel size you are using. The chain length is the number of panels connected. Note: currently only a horizontal chain of panels is supported.

Next, you need to go into the 2D Configuration and create a single matrix with the total size of your hub75 setup. e.g a chain of 2 panels with 32x32 pixels each, would be created as a 64x32 matrix in the 2D configuration page
