---
title: DMX Input
hide:
  # - navigation
  # - toc
---

### DMX Input

!!! info "Version Info"
    As of version v0.14.0-b25 MM-WLED supports DMX input via MAX485. This is great when ArtNet or e1.31/sACN over WIFI is not suitable 

#### features and limitations

* one universe (512 channels)

#### software setup

For the DMX feature to work, you'll need to use the V4 build varients.

#### hardware setup

The DMX output required the use of a MAX485 transceiver connected to the pins defined in setup of the ESP in order to produce DMX input.


You will need to use three GPIO pins that support output.

Do NOT use the pins on your ESP32 labelled RX and TX as your DMX pins!

* RX pin connects to RO
* TX pin connects to DI
* EN pin connects to both DE and RE

Connect the RS485 power pins as follows

* 5v or 3.3v pin to VCC
* GND to GND

#### background info


For information about the use of DMX with ESP8266, you might like to read [this](https://robertoostenveld.nl/art-net-to-dmx512-with-esp8266/) tutorial by [Robert Oostenveld](https://robertoostenveld.nl/). Note this is just background information about the hardware and you do not need any of the code listed here when using WLED output.

## questions

If you have further questions about this feature, you can ask on [DMX Input Discord](https://discord.com/channels/473448917040758787/1097792072762798110) or reach me via github (@netmindz) or via WLED Discord (netmindz).
