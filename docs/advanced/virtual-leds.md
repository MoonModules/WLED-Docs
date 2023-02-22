---
title: Virtual LEDs
hide:
  # - navigation
  # - toc
---

## Overview

Virtual LEDs allow you to "attach" LEDs from multiple ESPs to a main, controlling ESP. These LEDs can be added to an ESP just like physical pins.

On the controlling ESP, go to Config, LED Preferences. 

Select DDP RGB (Network) or ART-Net RGB (Network) as the LED type and enter the Length (number of LEDs on that remote ESP), then enter the ESPs IP address.

Multiple remote ESP's can be setup this way.

<img width="448" alt="image" src="https://user-images.githubusercontent.com/91013628/214262598-e7ce0907-ccad-4370-9d02-918efd20577c.png">

For DDP the controlling ESP must be running at least 0.13 firmware while the remotes can be older. As usual, best perfomance is obtained by using an ESP32 for the controlling device. You can use an ESP8266, but only with a small number of LEDs (<300).

Art-Net is only implemented in MoonModules 0.14.0.b1.18.

### DDP 


### Art-Net
🌜

Art-Net universe output starts at zero. This is not currently configurable in WLED. Zero is the commonly expected starting universe for Art-Net. Channel output starts at one and is not currently configurable in WLED. One is the expected first channel in Art-Net.

For RGB LEDs, a full universe (170 RGB pixels) produces 510 channels  - channels 511 and 512 will not be transmitted. This is common practice  in Art-Net transmit and most (all?) implementations will expect this.

Art-Net output follows xLights' implementation of packet sequence numbering and universe-channel alignment, and transmits in RGB order. The first pixel output data will always be 0:1:R, 0:2:G, 0:3:B for universe:channel:colorpart.

This Art-Net implementation does ignore the "always specify length of data as an even number" part of the official specifications. If you encounter this issue, please file a bug report. Even Art-Net themselves say that this has been widely ignored and receivers should not expect an even value in the data length part of the packet.
