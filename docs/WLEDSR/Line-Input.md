# I2S ADC for Line-In

Looking to add line-in with I2S support? You might want to try I2S ADC boards that use one of these chips: 
* [CirrusLogic WM8782](https://www.cirrus.com/products/wm8782/)
* [CirrusLogic CS5343](https://www.cirrus.com/products/cs5343-44/)
* [AKM AK5720](https://www.akm.com/eu/en/products/audio/audio-adc/ak5720et/) ([datasheet](https://www.akm.com/content/dam/documents/products/audio/audio-adc/ak5720vt/ak5720vt-en-datasheet.pdf))
* [Ti PCM1808](https://www.ti.com/product/PCM1808) or [Ti PCM1802](https://www.ti.com/product/PCM1802)

<p> &nbsp; </p>

 <img src="https://user-images.githubusercontent.com/91616163/193432590-176d20e8-2432-4eca-86f9-86cda91aa873.jpg" width="40%" height="40%" /> &nbsp; &nbsp; 
<img src="https://user-images.githubusercontent.com/91616163/197608486-cafcdf75-8039-4cb9-9d96-182d835c52c3.JPG" width="24%" height="24%" /> 


Many I2S ADC boards expect an additional MCLK signal ("Main Clock" aka "System Clock" aka "Master Clock" aka "Memory Clock").  MCLK is sometimes labelled SCLK for "system clock". For these boards with 4 data pins, use our `Generic I2S with MCLK` input driver, and connect MCLK pin to GPIO pin 0, 1, or 3 on ESP32.


##  TI PCM1808
<img src="https://user-images.githubusercontent.com/91616163/193432571-fb48bbff-e611-4235-bb47-5418f88c2c8d.jpg" width="20%" height="20%" />   &nbsp; &nbsp;

Top side: Right audio input, Audio Ground, Left audio input. 

Right side: The I2S connections -

* BCK = I2S SCK
* OUT = I2S SD
* LRC = I2S WS
* SCK = I2S MCLK (master clock)
* Ground
* 3.3v input

Left side: Format, Mode selector 0, Mode selector 1, ground, 3.3v input, and 5v input.

In WLED it's "Generic I2S with Mclk". You have 3 choices of what MCLK pin you can use - 0, 1, and 3. Pin 0 highly recommended as 1 ans 3 may already be in use

5v seems to NEED to be connected. You can connect it to 3.3v but it will glitch randomly. Put that pin on 5v for best function. 3.3v and ground are connected to the same pins on the right side, so you just need to connect one of each, on either side. 

MD1 and MD0 set master/slave modes. It defaults to slave (both pins are internally set to low), which is what you want for WLED. Don't connect these to anything.

FMY (format, FMT in the spec sheet - I assume the "Y" is a typo on the silkscreen) is a bit more interesting. By default it's pulled low internally, which the docs claim to be "I2S, 24-bit" - which will work fine as a default.

...however, pulling FMY "high" (connected to 3.3v) seems to make everything better in WLED.  According to the spec sheet, this moves the entire 24 bit sequence one pulse earlier ("left justified") and the responsiveness seems to be better overall in WLED.  The GEQ visual output is more "balanced" with the highs being better represented. The format of the 24 bits is unchanged - both are MSB first - but it seems to be better in WLED when the pin is pulled high.
