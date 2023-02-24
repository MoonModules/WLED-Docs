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

For RGB LEDs, a full universe (170 RGB pixels) produces 510 channels  - channels 511 and 512 will not be transmitted. This is common practice in Art-Net transmit and most (all?) implementations will expect this.

Art-Net output follows xLights' implementation of packet sequence numbering and universe-channel alignment, and transmits in RGB order. The first pixel output data will always be 0:1:R, 0:2:G, 0:3:B for universe:channel:colorpart.

This Art-Net implementation does ignore the "always specify length of data as an even number" part of the official specifications. If you encounter this issue, please file a bug report. Even Art-Net themselves say that this has been widely ignored and receivers should not expect an even value in the data length part of the packet.

### Background
By Troy

First there was DMX (DMX512). It was great for controlling lighting fixtures - "set light to red" sort of thing. "Pan head to the left". "Dim the lights."

Then someone decided that DMX should work over the network rather than RS485 networks (usually over an XLR cable).

So Art-Net and E1.31 were born. DDP came later and improved upon the idea, but DDP isn't as widely supported yet. 

All of these are the same premise as DMX512 - send packets of 8-bit numbers to remote systems. E1.31 and Art-Net are aligned with DMX512 and can send 512 channels per packet/universe, whereas DDP can send up to 1440 channels. 

THEN a bunch of idiots (us) got into the game with massive LED panels.

To send LED data over the network, we still use a network form of DMX. E1.31, Art-Net, and DDP are all "network DMX".

You can think of an LED strip (or matrix) as a LOT of dimmable lights:

You have a red dimmable light. 
You have a green dimmable light. 
You have a blue dimmable light.

That's channels 1,2, and 3 - and they makes up one RGB LED.

A DMX universe is 512 channels (1440 in DDP). You can fit 170 LEDs into 510 channels (170 LEDs each having 3 channels - R, G, and B) 
And then you skip to the next universe and start at channel 1 again.

The issue with Art-Net and E1.31 (and DMX512, really) is that the sequence of numbers are just a list of numbers. There's no context to these numbers in the packet so it's up to the receiving end to understand these numbers in a meaningful fashion. DDP can some context - RGB, RGBW, HSL, and grayscale are all possible to identify in addition to unstructured data. DDP can also specify the bits per pixel, allowing 1, 4, 8, 16, 24 or 32-bit values. DMX/Art-Net/E1.31 are always 8-bit, in the range of 0-255.

<h2>Using Art-Net/DMX/E1.31 to control WLED... controls</h2>

<img width="508" alt="image" src="https://user-images.githubusercontent.com/91013628/220875588-f5c6aa58-5e09-45e8-86f7-2d86e68d82a0.png">

When using Art-Net "Effect" mode in WLED, those 15 sliders in QLC+ send control data to those 15 parameters in the table. 
Slider 1 is master brightness.
Slider 2 is effect.
9,10,11 are R,G,B primary color.
etc.

Could you use QLC+ to send data to a matrix or strip? absolutely
You just need THREE sliders (R/G/B) for every LED.

<img width="982" alt="image" src="https://user-images.githubusercontent.com/91013628/220875991-d93083fd-6a56-41f1-aee0-d5a1e0f5e8c1.png">

1,2,3 = pixel 1. (set to red)
4,5,6 = pixel 2. (set to green)
7,8,9 = pixel 3. (set to blue)
10,11,12 = pixel 4. (set to white, all sliders up)

With a panel of 768 pixels, you only need... 2304 sliders to set them all. 😄 
This is with WLED set to "Multi RGB" in Art-Net.

All of those "DMX mode" settings tell WLED how to interperate the incoming DMX data (thru whatever Network DMX protocol you're using)

"Multi RGB" is for lighting lots of pixels.
"Effect" is for controlling the WLED instance itself. 
...and the others have their own special methods.
Jinx -> WLED works fine with any protocol, and WLED set to "Multi RGB"

WLED -> Jinx is... not exactly a thing, at least when using WLED network LED output. Jinx only takes "network DMX" as a remote control input, not LED input. 

DMX into WLED via a physical DMX wire (RS485): This would be equivalent to "Effect" (and will likely be based on that mapping) so that you could plug WLED boards into a DMX512 cable and have it "do a thing" when you push a slider on the lighting control board. (or more common now, the lighting control software) 

