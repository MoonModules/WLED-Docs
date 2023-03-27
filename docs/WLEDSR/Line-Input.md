# I2S ADC for Line-In

Looking to add line-in with I2S support? You might want to try I2S ADC boards that use one of these chips: 
* [CirrusLogic WM8782](https://www.cirrus.com/products/wm8782/)
* [CirrusLogic CS5343](https://www.cirrus.com/products/cs5343-44/)
* [AKM AK5720](https://www.akm.com/eu/en/products/audio/audio-adc/ak5720et/) ([datasheet](https://www.akm.com/content/dam/documents/products/audio/audio-adc/ak5720vt/ak5720vt-en-datasheet.pdf))
* [Ti PCM1808](https://www.ti.com/product/PCM1808) or [Ti PCM1802](https://www.ti.com/product/PCM1802)

<p> &nbsp; </p>

<img src="https://user-images.githubusercontent.com/91616163/193432571-fb48bbff-e611-4235-bb47-5418f88c2c8d.jpg" width="20%" height="20%" />   &nbsp; &nbsp;
 <img src="https://user-images.githubusercontent.com/91616163/193432590-176d20e8-2432-4eca-86f9-86cda91aa873.jpg" width="40%" height="40%" /> &nbsp; &nbsp; 
<img src="https://user-images.githubusercontent.com/91616163/197608486-cafcdf75-8039-4cb9-9d96-182d835c52c3.JPG" width="24%" height="24%" /> 


Many I2S ADC boards expect an additional MCLK signal ("Main Clock" aka "System Clock" aka "Master Clock" aka "Memory Clock").  MCLK is sometimes labelled SCLK for "system clock". For these boards with 4 data pins, use our `Generic I2S with MCLK` input driver, and connect MCLK pin to GPIO pin 0, 1, or 3 on ESP32.
