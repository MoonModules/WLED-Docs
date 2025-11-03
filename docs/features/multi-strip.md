---
title: Multi-strip Support
hide:
  # - navigation
  # - toc
---

## Multi strip support

Starting in WLED 0.12.0, you are able to use multiple LED outputs from one ESP board!
Pins and LED numbers can be easily configured in LED settings, you don't need to re-compile code for your specific setup. Custom binaries for multiple pins are now also a thing of the past!

There are a few tips and recomendations to keep in mind when designing your setup:

### General

- It is highly recommended to use an ESP32 when using more than 1 output
- You may freely choose the LEDs type, pin numbers, length and color order of your LED strips at runtime in the LED settings page
- Highly recommended to size power supply correctly according to your setup and disable the WLED brightness limiter setting to increase framerate with very large LED counts
- Most strip types have yet to be tested. Add confirmed working below:
- Confirmed working: WS281x, SK6812 RGBW, PWM white

### ESP8266

- There is a maximum of 3 strips supported.
- It is highly recommended to use two specific LED pins, GPIO1 (TX) and GPIO2 (D4), since they allow for hardware driving.
- It is recommended to use 512 LEDs/pin for good performance for a total of 1024 LEDs.
- 800 LEDs/pin for a total of 1600 has been confirmed working, but is not recommended for good performance and reliability.
- Using GPIO1 will disable serial debugging. If you need it, you can't use a strip on this pin.
- GPIO3 (RX) is the third pin that allows hardware driving on ESP8266. However, it uses 5 times as much memory per LED as GPIO 1 and 2, so use it only for low LED counts (recommended <50)
- You can use any other pin, but it will use the bitbang method, which is not recommended for reliability. It is best to stick to GPIO 1, 2, and if need be, 3.
- Using pin GPIO16 for WS2812b LEDs did not work in my testing.
- ESP8266 can calculate about 15k LEDs per second (that means 250LEDs @~60fps, 500 LEDs @~30fps, 1000 LEDs @~15fps)
- The LED settings will give you a bar that shows how much memory you can allocate.

### ESP32

- There is a maximum of 10 strips supported on "classic" ESP32 (dual core) boards. In audioreactive builds, you can use up to 9, because the audio input driver needs one of the hardware units that is normally available for driving LEDs.
 - * "classic" ESP32: 10 led strips (9 with audioreactive)
 - * ESP32-S3: 4 led strips
 - * ESP32-S2: 5 led strips (4 with audioreactive)
 - * ESP32-C3: 2 led strips
- Contrary to the ESP8266, the pin usage does not matter on ESP32, feel free to use any available pin
- For perfect performance, it is recommeded to use 512 LEDs/pin with 4 outputs for a total of 2048 LEDs.
- For very good performance, it is recommended to use 800 LEDs/pin with 4 outputs for a total of 3200 LEDs.
- For good performance, you can use 1000 LEDs/pin with 4 outputs for a total of 4000 LEDs.
- For okay performance, you can use 1000 LEDs/pin with 5 outputs for a total of 5000 LEDs.
- For okay performance, you can use 800 LEDs/pin with 6 outputs for a total of 4800 LEDs.


#### Performance

In WLED-MM, classic ESP32 can calculate about *200k-300k LEDs* per second

- This means 1,000 LEDs at 250 frames per second, 2,000 LEDs at 120 frames per second, or 4,000 LEDs at 70 frames per second.
- WLED-MM framerates can even be faster if effects don't redraw each LED in each frame.
- However these maximum values can only be achieved with HUB75, or when you distribute your LEDs over several output pins.
- 4 output pins seem to be the sweet spot (see below).
- With many output pins the ESP32 will be very busy driving parallel outputs, so it can't calculate as many LEDs.

Keep in mind that the limiting factor is usually the speed of the ws2812b protocol - each strip (=output pin) runs an 800kz serial protocol, and each pixel needs 24 bits (RGB color).
You can calculate the max possible speed - per output pin - with this formula : 

 ``800000 / 24 / strip_length_in_pixels `` = max frames per second.
  For RGB+White (sk6812), replace "24" with "32".

- 144 LEDs per output pin -> max 230 fps
- 240 LEDs per output pin -> max 139 fps
- 320 LEDs per output pin -> max 104 fps
- 500 LEDs per output pin -> max 67 fps
- 800 LEDs per output pin -> max 42 fps
- 1000 LEDs per output pin -> max 33 fps
- 2000 LEDs per output pin -> max 17 fps


### Virtual LEDs (DDP and Art-Net 🌜)

See [Virtual Leds](/advanced/ddp)
