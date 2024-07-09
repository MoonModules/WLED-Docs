---
title: HUB75 support
---

WLED-MM now features support for LED matrix panels using the HUB75 format

You can use either a regular ESP32 with a suitable adapter board such as [ESP32 Trinity](https://esp32trinity.com/) or [rorosaurus/esp32-hub75-driver](https://github.com/rorosaurus/esp32-hub75-driver) or the dedicated [Adafruit Matrix Portal S3](https://www.adafruit.com/product/5778)

This support is supplied by [ESP32-HUB75-MatrixPanel-DMA](https://github.com/mrcodetastic/ESP32-HUB75-MatrixPanel-DMA?tab=readme-ov-file) so see here for more details about supported hardware

Support for HUB75 in WLED-MM should be considered experimental at the moment, but we welcome early feedback on this new feature

## Configuration
### Adafruit Matrix Portal S3
Please use the dedicated adafruit_matrixportal_esp32s3 build as this is pre-configured for HUB75 output
### Generic ESP32 support
You need to use a build with WLED_ENABLE_HUB75MATRIX defined, for example, esp32_4MB_V4_S.

If you are using a board such as the ESP32 Trinity or other boards defined for the default pinout of the ESP32-HUB75-MatrixPanel-DMA driver, this is selected by default

If you are using the rorosaurus/esp32-hub75-driver or any other board using the SmartMatrix default pinout then you will need to do a custom build with ESP32_FORUM_PINOUT defined

If you are using any other config, you currently need to edit wled00/bus_manager.cpp to add a new elif block and define to your build - it is not possible to set the pin config in LED preferences at the moment
