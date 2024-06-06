# I2S ADC for Line-In

If you want the best experience, then Line-In using I2S will give the best quality. As you are getting a clean audio feed the squelch value should be set to 1 to start with, and a gain of 1 is also likely a good starting point. Automatic Gain Control (AGC) set to "Normal" is still recommended, but not strictly required.

Looking to add line-in with I2S support? You might want to try I2S ADC boards that use one of these chips: 
* [CirrusLogic WM8782](https://www.cirrus.com/products/wm8782/)
* [CirrusLogic CS5343](https://www.cirrus.com/products/cs5343-44/)
* [AKM AK5720](https://www.akm.com/eu/en/products/audio/audio-adc/ak5720et/) ([datasheet](https://www.akm.com/content/dam/documents/products/audio/audio-adc/ak5720vt/ak5720vt-en-datasheet.pdf))
* [Ti PCM1808](https://www.ti.com/product/PCM1808) or [Ti PCM1802](https://www.ti.com/product/PCM1802)
* [ES8388](https://datasheet.lcsc.com/lcsc/1912111437_Everest-semi-Everest-Semiconductor-ES8388_C365736.pdf)
* [WM8978](https://www.mouser.com/datasheet/2/76/WM8978_v4.5-1141768.pdf)

Many I2S ADC line-in boards expect an additional MCLK signal ("Main Clock" aka "System Clock" aka "Master Clock" aka "Memory Clock").  MCLK is sometimes labelled SCLK for "system clock". For these boards with 4 data pins, use the AudioReactive `Generic I2S with MCLK` input option, and connect MCLK pin to GPIO pin 0 on the original ESP32. 

**NOTE:* Technically GPIO 1 and 3 will work on the original ESP32 for MCLK, but these are most often in use for the serial console. If you're using an MCLK-required line-in board on an ESP32-S3 (and possibly other ESP32-XX boards) then the MCLK can be any free GPIO pin. WLED will generally show you which pins are allowed for MCLK on your board.

## Pmod I2S2
<img src="https://user-images.githubusercontent.com/91616163/197608486-cafcdf75-8039-4cb9-9d96-182d835c52c3.JPG" width="24%" height="24%" />

* Jumper: Set to "Slave"

[Data Sheet and Information](https://digilent.com/reference/pmod/pmodi2s2/start)

## WM8782
<img src="https://user-images.githubusercontent.com/91616163/193432590-176d20e8-2432-4eca-86f9-86cda91aa873.jpg" width="40%" height="40%" /> &nbsp; &nbsp; 
 
Buy: [AliExpress](https://www.aliexpress.com/item/32989916894.html)

* Remove jumper from MLCK
* DIP switch - SLAVE
* DIP switch - 24 bit

[Data Sheet](https://d3uzseaevmutz1.cloudfront.net/pubs/proDatasheet/WM8782_v4.8.pdf)

## TI PCM1808
<img src="https://user-images.githubusercontent.com/91616163/193432571-fb48bbff-e611-4235-bb47-5418f88c2c8d.jpg" width="20%" height="20%" />   &nbsp; &nbsp;

Buy: [Amazon](https://a.co/d/3IHJWjV) or [AliExpress](https://a.aliexpress.com/_EydzFDt) 

Top side: Right audio input, Audio Ground, Left audio input. 

Right side: The I2S connections -

* BCK = I2S SCK
* OUT = I2S SD
* LRC = I2S WS
* SCK = I2S MCLK (master clock)
* Ground = ground
* 3.3v input = 3.3v

Left side: Feature settings and 5v input:

* Format = Currently recommended set to 3.3v (see below) or Not Connected.
* Mode selector 0 = Not connected
* Mode selector 1 = Not connected
* Ground = alternate ground, you only need one
* 3.3v input = alternate 3.3v input, you only need one
* 5v input = 5v input for audio circuits. Connect to 5v

In WLED AudioReactive settings you will need to use `Generic I2S with MCLK`. You have 3 choices of what MCLK pin you can use - 0, 1, and 3. Pin 0 highly recommended as 1 as 3 will likely be in use on the original ESP32 for the serial console.

5v seems to NEED to be connected. You can connect it to 3.3v but it will glitch randomly. Put that pin on 5v for best function. 

3.3v and ground are connected to the same pins on the right side - just need to connect one of each, on either side. 

MD1 and MD0 set master/slave modes. It defaults to slave (both pins are internally set to low), which is what you want for WLED. Don't connect these to anything.

FMY (format, FMT in the spec sheet - I assume the "Y" is a typo on the silkscreen) is a bit more interesting. By default it's pulled low internally, which the docs claim to be "I2S, 24-bit" - which will work fine as a default.

...however, pulling FMY "high" (connected to 3.3v) seems to make everything better in WLED.  According to the spec sheet, this moves the entire 24 bit sequence one pulse earlier ("left justified") and the responsiveness seems to be better overall in WLED.  The GEQ visual output is more "balanced" with the highs being better represented. The format of the 24 bits is unchanged - both are MSB first - but it seems to be better in WLED when the pin is pulled high.

## ES8388

This audio chip reqires I2C commands to initialize properly. "Line-in mode" has been hard-coded into the initialization and will be used when "ES8388" is selected.

The on-board microphones are not currently supported - line-in is much better regardless. 

* [ESP32 Lyra-T V4.3](https://docs.espressif.com/projects/esp-adf/en/latest/design-guide/dev-boards/board-esp32-lyrat-v4.3.html)

<img src="https://user-images.githubusercontent.com/91616163/193413089-6f71193c-d8db-4185-9de3-c8b4005431c1.jpg" width="40%" height="40%" />

* [Ai-Thinker ESP32 Audio Kit v2.2](https://docs.ai-thinker.com/en/esp32-audio-kit)

<img src="https://user-images.githubusercontent.com/91616163/193413239-e3fd9567-a64d-464c-bdc6-2a2ce69c0df5.png" width="40%" height="40%" />
Note: the underside of ESP32 overhang shows ESP32-A1S 2974

Line-in should be internally routed to line-out, allowing these boards to be used in the middle of a line-level signal path.

### Pin Config

The LyraT v4.3 and some AiThinker v2.2 boards use the following pin config:

* Type: ES8388
* IS2 SD = 35
* I2S WS = 25
* I2S SCK = 5
* I2S MCLK = 0
* I2C SDA = 18
* I2C SCL = 23  

If the above doesn't work for AiThinker v2.2 boards use a chip with the following pins, use if you see errors about I2C:

Note: the underside of ESP32 overhang shows ESP32-A1S B221 and B238 on two boards with this config - the "B" or "B2" may be hints as to revision. 

* Type: ES8388
* IS2 SD = 35
* I2S WS = 25
* I2S SCK = 27
* I2S MCLK = 0
* I2C SDA = 33
* I2C SCL = 32

## WM8978

This audio chip reqires I2C commands to initialize properly. "Line-in mode" has been hard-coded into the initialization and will be used when "WM8978" is selected.

The on-board microphones are not currently supported - line-in is much better regardless. 

Support for the WM8978 chipset is derived from the [Puca DSP board](https://github.com/ohmic-net/puca_dsp):

![image](https://github.com/MoonModules/WLED-Docs/assets/5659019/a97d0ecc-a024-42c2-99f3-aef11c17ec35)

Curently the Puca DSP on-board microphones may leak some sound in **extremely** loud environments, but the line-in will overpower this signal when presented. This has been minimized with settings.

Line-in should be internally routed to line-out, allowing this board to be used in the middle of a line-level signal path.

### Pin Config

The Puca DSP board pins are as follows:

* Type: WM8978
* I2S SD = 27
* I2S WS = 25
* I2S SCK = 23
* I2S MCLK = 0
* I2C SDA = 19 (set in global)
* I2C SCL = 18 (set in global)
 
