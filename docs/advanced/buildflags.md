---
title: WLED Build Flags
hide:
  # - navigation
  # - toc
---

# WLED MoonModules Build Flags

Version at time of page update: WLEDMM 0.14.0-b15.23 - commit 244a613

Sourced by: <a href="https://discordapp.com/users/365874439801274391">Sören#5281</a><br />
Organized and updated by: <a href="https://discordapp.com/users/701524773124964383">Troy#2642</a>

Flags/functions specific to WLED MoonModules are denoted with the ☾ icon.

## Basic Usage

### In "my_config.h" or in the C/C++ code

For entries with no parameter, prefix with `#define` like `#define WLED_DEBUG`

For entries with a numeric parameter, use the syntax of `#define LEDPIN 16`

For non-numeric entries use quotes like `#define WLED_AP_SSID "MY-WLED-AP"`

### In "platformio.ini" or "platformio_override.ini"

For items with no parameter, prefix with `-D` like `-D WLED_DEBUG`

For entries with a numeric parameter, use the syntax of `-D LEDPIN=16`

For non-numeric entries use **both** types of quotes like `-D SERVERNAME='"WLED-C3"'`

## The Long List of Flags

### Common WLED buildflags

| Flag | Description |
| --- | --- |
| WLED_RELEASE_NAME | Sets the internal release name of the build. Also used to set bin filenames in PlatformIO builds. |
| WLED_MAX_USERMODS | defaults to 4 on esp8266 and 6 on ESP32 |
| WLED_MAX_BUSSES | defaults to 3 on esp8266, 10 on esp32 without AR, 8 on esp32 with AR, 6 on ESP32S3, 6 esp32S2 with AR, 7 on esp32s2 without AR, 3 on ESP32C3 |
| WLED_MAX_BUTTONS | defaults to 2 on esp8266 and 4 on esp32 |
| WLED_MAX_LEDMAPS | defaults to 10 on esp8266 and 156 on esp32 |
| MAX_LEDS | defaults to 1664 on esp8266 and 8192 on esp32 |
| MAX_LED_MEMORY | defaults to 4000 on esp8266 and 32000 on esp32C3 and esp32S2, 64000 on ESP32 and ESP32S3 |
| MAX_LEDS_PER_BUS | defaults to 2048 |
| WLED_USE_ETHERNET | enables Ethernet support |
| ABL_MILLIAMPS_DEFAULT | 0 to disable minimum is 250, defaults to 850 |
| WLED_PWM_FREQ | defaults to 880 on esp8266 and 19531 on esp32 |
| LEDPIN | defaults to GPIO2 on esp8266 and GPIO16 on esp32 |
| WLED_ENABLE_DMX | Enables hardware DMX input/output functions |
| DEFAULT_LED_COUNT | defaults to 30 |
| HW_PIN_SCL | defaults to SCL value |
| HW_PIN_SDA | defaults to SDA value |
| HW_PIN_CLOCKSPI | defaults to SCK |
| HW_PIN_DATASPI | defaults to MOSI |
| HW_PIN_MISOSPI | defaults to MISO |
| WLED_USE_REAL_MATH | use math and not lookuptables |
| DEFAULT_LED_TYPE | defaults to TYPE WS2812_RGB |
| PIXEL_COUNTS | defaults to DEFAULT_LED_COUNT |
| DATA_PINS | defaults to LEDPIN |
| DEFAULT_LED_COLOR_ORDER | defaults to COL_ORDER_GRB |
| WLED_WATCHDOG_TIMEOUT | set the whatchdog timout in milliseconds, default to 0 (deactivated) |
| WLED_DISABLE_BROWNOUT_DET | disables ESP32 brownout detector (off by default) |
| CLIENT_SSID | Sets the default WiFi SSID to connect to |
| CLIENT_PASS | Sets the default WiFi password to connect with |
| WLED_AP_SSID | Sets the name of the internal WiFI AP |
| WLED_AP_PASS | Set the default password for the internal WiFi AP | 
| SPIFFS_EDITOR_AIRCOOOKIE | If you are not using the Aircoookie fork of the ESPAsyncWebserver library and using upstream,  puts your WiFi password at risk of being served by the filesystem. Comment out this error message to build regardless. |
| WLED_VERSION | defaults to "dev" |
| BTNPIN | Sets the first button pin GPIO |
| RLYPIN | Sets the relay GPIO |
| RLYMDE | 1=active high, 0= active low |
| IRPIN | Sets the IR receiver GPIO |
| SERVERNAME | defaults to "WLED" |
| WLED_DEBUG_HOST | to send debug messages over network to host 192.168.x.y - FQDN is also possible |
| WLED_DEBUG_PORT | defaults to 7868 |
| WLED_AP_SSID_UNIQUE | Adds the MAC address to the WLED AP SSID if enabled, so everything doen't show up as "WLED-AP" |
| WLED_DEBUG | Turns on debug messages to the serial console |
| LED_BUILTIN | Fix for turning off onboard LED breaking bus |
| WLED_USE_IC_CCT | ...something about how LED strips with warm+cool white LEDS work |
| WLED_MAX_CCT_BLEND | How warm and cool white RGBWW LEDs are managed | 
| WLED_ADD_EEPROM_SUPPORT | Enable saving key settings to EEPROM (actually 512 bytes of Flash memory, not literal EEPROM) |
| ESP32_DATA_IDLE_HIGH | If enabled, RMT idle level is set to HIGH when off to prevent leakage current when using an N-channel MOSFET to toggle LED power |
| WLED_ENABLE_SIMPLE_UI | Enables a simplified web UI. Used mostly on small devices like the ES8266 | 
| WLED_ENABLE_MQTT | Enables WLED to send internals and usermod data via [MQTT](https://mqtt.org/) |
| WLED_ENABLE_JSONLIVE | peek LED output via /json/live (WS binary peek is always enabled) |
| WLED_DEBUG_FS | filesystem specific debugging |
| WLED_DEBUG_IMPROV | Debugging for Improv serial |
| WLED_ENABLE_LOXONE |  Enable [Loxone](https://www.loxone.com/) support |
| WLED_ENABLE_WEBSOCKETS | Enable websockets |
| WLED_ENABLE_ADALIGHT | Enables [AdaLight](https://learn.adafruit.com/adalight-diy-ambient-tv-lighting/overview) support |
| WLED_DEBUG_NTP | Enable NTP debugging |
| WLED_ENABLE_PIXART | Enable new PixArt support |

### PSRAM 

| Flag | Description |
| --- | --- |
| BOARD_HAS_PSRAM | Enables PSRAM during compilation. Board needs to have PSRAM, not all of them do. |
| WLED_USE_PSRAM | Uses PSRAM for several functions. Often slows down LEDs. |
| WLED_USE_PSRAM_JSON | ☾ Uses PSRAM only for the JSON decoding buffer. Does not slow down LEDs. This setting also increases JSON_BUFFER_SIZE from 24576 to 60000 when enabled on ESP32 and ESP32-S3 (and 48000 on ESP32-S2 and -C3), allowing for bigger LED remapping files. |

## MoonModules ☾ Specific Flags

### Artifx ☾

| Flag | Description |
| --- | --- |
| ARTI_DEBUG | Enables ArtiFX debug |
| ARTI_ANDBG | ArtiFX debugging |
| ARTI_RUNLOG | if set on arduino this will create massive amounts of output (as ran in a loop) |
| ARTI_PRINT | will show the printf calls |
| ARTI_ERRORWARNING | shows lexer, parser, analyzer and interpreter errors |
| ARTI_MEMORY | to do analyses of memory usage, trace memoryleaks (works only on arduino) |
| OPTIMIZED_TREE | Optimized tree function for ArtiFX |

### Pinmanager ☾

| Flag | Description |
| --- | --- |
| SOC_ADC_CHANNEL_NUM | Sets ADC0 or ADC1 for I2C functions |
| MPU6050_INT_GPIO | Sets the interrupt pin for the MPU6050. Also uses I2C. Does not work when Four Line Display is enabled. |

### Internals ☾

| Flag | Description |
| --- | --- |
| WLED_DEBUG_MATH | Prints out results of some more complex math functions to the serial console. |

### MoonModules Usermods ☾

| Flag | Description |
| --- | --- |
| USERMOD_MPU6050_IMU | Enables the Motion Processing Unit - MPU6050 |
| ARTIFX | Enables the runtime effects scripting interperter |
| WEATHER | Enables the weather display usermod |
| USERMOD_GAMES | Enables effects/games that use the MPU6050 chip |
| USERMOD_FASTLED | Enables extra effects with a Creative Commons license. Do not enable this if using WLED in a for-profit manner. |

## Generic WLED Flags

### WLED Usermods

| Flag | Description |
| --- | --- |
| USERMOD_BATTERY | usermod_v2_Battery.h |
| USERMOD_DALLASTEMPERATURE | usermod_temperature.h |
| USERMOD_SHT | usermod_sht.h |
| USERMOD_SN_PHOTORESISTOR | usermod_sn_photoresistor.h |
| USERMOD_PWM_FAN | usermod_PWM_fan.h |
| USERMOD_BUZZER | usermod_v2_buzzer.h |
| USERMOD_SENSORSTOMQTT | usermod_v2_SensorsToMqtt.h |
| USERMOD_PIRSWITCH | usermod_PIR_sensor_switch.h |
| USERMOD_MODE_SORT | usermod_v2_mode_sort.h |
| USERMOD_BH1750 | usermod_BH1750.h |
| USERMOD_BME280 | usermod_bme280.h |
| USERMOD_FOUR_LINE_DISPLAY | usermod_v2_four_line_display.h |
| USERMOD_ROTARY_ENCODER_UI | usermod_v2_rotary_encoder_ui.h |
| USE_ALT_DISPlAY | Alt versions of the two above instead of normal. You likely want to use this if you are using the above two features. |
| USERMOD_AUTO_SAVE | usermod_v2_auto_save.h |
| USERMOD_DHT | usermod_dht.h |
| USERMOD_VL53L0X_GESTURES | usermod_vl53l0x_gestures.h |
| USERMOD_ANIMATED_STAIRCASE | Animated_Staircase.h |
| USERMOD_MULTI_RELAY | usermod_multi_relay.h |
| USERMOD_RTC | usermod_rtc.h |
| USERMOD_ELEKSTUBE_IPS | usermod_elekstube_ips.h |
| USERMOD_ROTARY_ENCODER_BRIGHTNESS_COLOR | usermod_rotary_brightness_color.h |
| RGB_ROTARY_ENCODER | rgb-rotary-encoder.h |
| USERMOD_ST7789_DISPLAY | ST7789_Display.h |
| USERMOD_SEVEN_SEGMENT | usermod_v2_seven_segment_display.h |
| USERMOD_SSDR | usermod_seven_segment_reloaded.h |
| USERMOD_CRONIXIE | usermod_cronixie.h |
| QUINLED_AN_PENTA | quinled-an-penta.h |
| USERMOD_WIZLIGHTS | wizlights.h |
| USERMOD_WORDCLOCK | usermod_v2_word_clock.h |
| USERMOD_MY9291 | usermode_MY9291.h |
| USERMOD_SI7021_MQTT_HA | usermod_si7021_mqtt_ha.h |
| USERMOD_SMARTNEST | usermod_smartnest.h |
| USERMOD_AUDIOREACTIVE | audio_reactive.h |
| USERMOD_ANALOG_CLOCK | Analog_Clock.h |
| USERMOD_PING_PONG_CLOCK | usermod_v2_ping_pong_clock.h |
| USERMOD_ADS1115 | usermod_ads1115.h |
| USERMOD_BOBLIGHT | boblight.h |
| USERMOD_PWM_OUTPUTS | usermod_pwm_outputs.h |
| SD_ADAPTER | usermod_sd_card.h |
| USERMOD_KLIPPER_PERCENTAGE | usermod_v2_klipper_percentage.h

### Disable Features

| Flag | Description
| --- | ---
| WLED_DISABLE_OTA | Disables the feature to update firmware over the web interface. OTA is not possible for boards with 2MB flash only (like some Ai-Thinker ESP32-C3-12F models). |
| WLED_DISABLE_ALEXA | Disables [Amazon Alexa](https://g.co/kgs/7HHsPQ) support |
| WLED_DISABLE_HUESYNC | Disables the [Philips Hue](https://www.philips-hue.com/) support |
| WLED_DISABLE_INFRARED | Disables Infrared support - also useful to add `lib_ignore = IRremoteESP8266` to your platformio.ini or platformio_override.ini file |
| WLED_DISABLE_WEBSOCKETS | Disables the websockets |
| WLED_DISABLE_MQTT | Disables MQTT support. Warning: This may break your build unless you disable several other things as well. |
| WLED_DISABLE_SOUND | Disables sound features... but why would you do that? :D |
| WLED_DISABLE_2D | Disables 2D Features |
| WLED_DISABLE_LOXONE | Disable [Loxone](https://www.loxone.com/) support |

### Audio Responsive build flags

| Flag | Description |
| --- | --- |
| SR_SQUELCH | Sets the default squelch setting. Recommend 10 |
| SR_GAIN | Sets the defauly gain setting. Recommend 40 |
| AUDIOPIN | Analog audio pin |
| SR_DMTYPE | 0=none/disabled/analog ; 1=generic I2S |sd/data/dout
| I2S_SDPIN | Default I2S sd/data/dout input pin | pin
| I2S_WSPIN | Default I2S ws/clk/lrck pin |
| I2S_CKPIN | Default I2S sck/bclk pin |
| MCLK_PIN | Default I2S master clock/mclk pin |
| I2S_USE_16BIT_SAMPLES | Use if I2S input are already 16-bit. Likely not the case for most setups. |
| ES7243_SDAPIN | I2C SDA pin for ES7243 boards |
| ES7243_SCLPIN | I2C SCL pin for ES7243 boards |
| ES7243_ADDR | Sets the ES7243 I2c address. Default is usually correct. |
| ES8388_ADDR | Sets the ES8388 I2C address. Default is usually correct. |
| SR_DEBUG | Turns on sound-reactive specific debug messages |
| UM_AUDIOREACTIVE_USE_NEW_FFT | Turns on the new FFT code. ☾ Should be the default currently in most builds. |
| MIC_LOGGER | Turns on mic logging for debug purposes. You may be able to graph this output. |
| FFT_SAMPLING_LOG | FFT sampling debug log.|
| I2S_USE_RIGHT_CHANNEL | Tells I2S to use the right channel. Defaults to the left. |
| I2S_SAMPLE_DOWNSCALE_TO_16BIT | Enabled by default unless `I2S_USE_16BIT_SAMPLES` is defined. |

### Battery usermod

| Flag | Description |
| --- | --- |
| USERMOD_BATTERY_MEASUREMENT_PIN | Pin to measure the voltage, defaults to GPIO35 on ESP32 and A0 on ESP8266 |
| USERMOD_BATTERY_MEASUREMENT_INTERVAL | Interval to measure voltage in ms, defaults to 30s |
| USERMOD_BATTERY_MIN_VOLTAGE | Minimal voltage in volt, defaults to 3.2V if use lipo and min voltage is not set, if min voltage is not set and use lipo is set the dafault is 2.6V |
| USERMOD_BATTERY_USE_LIPO | Use LiPo discharge curve calculations |
| USERMOD_BATTERY_MAX_VOLTAGE | Max voltage in volt, defaults to 4.2V if not set |
| USERMOD_BATTERY_TOTAL_CAPACITY | capacity in mAh defaults to 3100mAh if not set |
| USERMOD_BATTERY_CALIBRATION | offset or calibration value to fine tune the calculated voltage |
| USERMOD_BATTERY_AUTO_OFF_ENABLED | auto-off feature, defaults to true |
| USERMOD_BATTERY_AUTO_OFF_THRESHOLD | Percentage theshold to turn power off |
| USERMOD_BATTERY_LOW_POWER_INDICATOR_ENABLED | low power indication feature, defaults to true |
| USERMOD_BATTERY_LOW_POWER_INDICATOR_PRESET | preset to use when low power threshold is hit - defaults to 0 |
| USERMOD_BATTERY_LOW_POWER_INDICATOR_THRESHOLD | percent - defaults to 20 |
| USERMOD_BATTERY_LOW_POWER_INDICATOR_DURATION | seconds - defaults to 5 |

### BH1750 usermod

| Flag | Description |
| --- | --- |
| USERMOD_BH1750_MAX_MEASUREMENT_INTERVAL | the max frequency to check photoresistorin milliseconds, 10 seconds |
| USERMOD_BH1750_MIN_MEASUREMENT_INTERVAL | the min frequency to check photoresistor in milliseconds, 500 ms |
| USERMOD_BH1750_FIRST_MEASUREMENT_AT | how many milliseconds after boot to take first measurement, 10 seconds |
| USERMOD_BH1750_OFFSET_VALUE | only report if differance grater than offset value, default 1 |

### BOBlight usermod

| Flag | Description |
| --- | --- |
| BOB_PORT | Boblight port, defaults to 19333 |

### Buzzer usermod

| Flag | Description |
| --- | --- |
| USERMOD_BUZZER_PIN | Buzzer pin, defaults to GPIO32 |

### DHT usermod

| Flag | Description |
| --- | --- |
| USERMOD_DHT_DHTTYPE | 11=DHT 11, 21=DHT 21, 22:DHT 22 (AM2302), AM2321 *** default |
| USERMOD_DHT_MEASUREMENT_INTERVAL | the frequency to check sensorin milliseconds, 1 minute |
| USERMOD_DHT_FIRST_MEASUREMENT_AT | how many seconds after boot to take first measurementin milliseconds, 90 seconds |
| USERMOD_DHT_PIN | defaults to 21 onm ESP32 and 4 on esp8266 |
| USERMOD_DHT_MQTT | Publish measurements to the MQTT broker |
| USERMOD_DHT_STATS | For debug, report delay stats |
| USERMOD_DHT_CELSIUS | Display temperatures in Celcius |

### BME280 usermod

| Flag | Description |
| --- | --- |
| Celsius | Display temperatures in Celcius |

### Enclosure usermod

| Flag | Description |
| --- | --- |
| Celsius | Display temperatures in Celcius |

### MQTTSWITCH usermod

| Flag | Description |
| --- | --- |
| MQTTSWITCHPINS | define MQTTSWITCHPINSe.g. -D MQTTSWITCHPINS="12, 0, 2" |
| MQTTSWITCHINVERT | invert the switch pins, default all active high |
| MQTTSWITCHDEFAULTS | default behavior, default all off |

### Multi Relay usermod

| Flag | Description |
| --- | --- |
| MULTI_RELAY_MAX_RELAYS | default to 4 |
| MULTI_RELAY_PINS | defaults to -1 |

### MY92XX usermod

| Flag | Description |
| --- | --- |
| DEBUG_MY92XX | Enable Debug |

### PIR usermod

| Flag | Description |
| --- | --- |
| PIR_SENSOR_PIN | defaults to GPIO23 on ESP32 and GPIO13 on ESP8266 |
| PIR_SENSOR_OFF_SEC | in milliseconds, defaults to 600ms |
| USERMOD_PIR_SENSOR_SWITCH | Enables PIR Usermod |

### PWM Fan usermod

| Flag | Description |
| --- | --- |
| TACHO_PIN | defaults to -1 |
| PWM_PIN | defaults to -1 |

### PWM OUTPUT usermod

| Flag | Description |
| --- | --- |
| USERMOD_PWM_OUTPUT_PINS | default to 3 |

### Photoresistor usermod

| Flag | Description |
| --- | --- |
| USERMOD_SN_PHOTORESISTOR_MEASUREMENT_INTERVAL | the frequency to check photoresistor in milliseconds, 10 seconds |
| USERMOD_SN_PHOTORESISTOR_FIRST_MEASUREMENT_AT | how many milliseconds after boot to take first measurement, 10 seconds |
| USERMOD_SN_PHOTORESISTOR_REFERENCE_VOLTAGE | supplied voltage |
| USERMOD_SN_PHOTORESISTOR_ADC_PRECISION | defaults to 1024 |
| USERMOD_SN_PHOTORESISTOR_RESISTOR_VALUE | defaults to 10k |
| USERMOD_SN_PHOTORESISTOR_OFFSET_VALUE | only report if differance grater than offset value, defaults to 5 |

### SD card usermod

| Flag | Description |
| --- | --- |
| WLED_USE_SD_MMC | Use when SD card is connected via MMC |
| WLED_USE_SD_SPI | Use when SD card is connected via SPI. Use the usermode page to set SPI pins |
| SD_ADAPTER | Enables SD card functionality. |

### ST7790 usermod

| Flag | Description |
| --- | --- |
| USER_SETUP_LOADED | Detects if an external user setup file for the display was used in the library code itself |
| ST7789_DRIVER | Enables ST7789 driver |
| TFT_WIDTH | TFT display width |
| TFT_HEIGHT | TFT display height |
| TFT_MOSI | Display MOSI pin |
| TFT_SCLK | Display SCLK pin |
| TFT_DC | Display DC pin |
| TFT_RST | Display reset pin |
| LOAD_GLCD | Font 1. Original Adafruit 8 pixel font needs ~1820 bytes in FLASH. Default enabled. |
| LOAD_FONT2 | Font 2. Small 16 pixel high font, needs ~3534 bytes in FLASH, 96 characters |
| LOAD_FONT4 | Font 4. Medium 26 pixel high font, needs ~5848 bytes in FLASH, 96 characters |
| LOAD_FONT6 | Font 6. Large 48 pixel font, needs ~2666 bytes in FLASH, only characters 1234567890:-.apm |
| LOAD_FONT7 | Font 7. 7 segment 48 pixel font, needs ~2438 bytes in FLASH, only characters 1234567890:. |
| LOAD_FONT8 | Font 8. Large 75 pixel font needs ~3256 bytes in FLASH, only characters 1234567890:-. | 
| LOAD_FONT8N | Font 8. Alternative to Font 8 above, slightly narrower, so 3 digits fit a 160 pixel TFT | 
| LOAD_GFXFF | FreeFonts. Include access to the 48 Adafruit_GFX free fonts FF1 to FF48 and custom fonts | 
| TFT_BL | Display backlight pin |

### Stairway whipe usermod

| Flag | Description |
| --- | --- |
| STAIRCASE_WIPE_OFF | If enabled, fade out versus doing a reverse wipe in the effect | 

### Temperature usermod

| Flag | Description |
| --- | --- |
| TEMPERATURE_PIN | defaults to 18 on ESP32 and 14 on ESP8266 |
| USERMOD_DALLASTEMPERATURE_MEASUREMENT_INTERVAL | the frequency to check temperature in milliseconds, 1 minute |

### TTGO T-Display

| Flag | Description |
| --- | --- |
| TFT_DISPOFF | defaults to 0x28 |
| TFT_SLPIN | defaults to 0x10 |

### autosave usermod

| Flag | Description |
| --- | --- |
| AUTOSAVE_AFTER_SEC | in seconds, default 15s |
| AUTOSAVE_PRESET_NUM | defaults to 250 |
| USERMOD_AUTO_SAVE_ON_BOOT | defaults to false |

### four line display usermod

| Flag | Description |
| --- | --- |
| FLD_PIN_SCL | defaults to i2c_scl value |
| FLD_PIN_SDA | defaults to i2c_sda value |
| FLD_PIN_CLOCKSPI | defaults to spi_sclk value |
| FLD_PIN_DATASPI | defaults to spi_mosi value |
| FLD_PIN_CS | defaults to spi_cs value |
| FLD_PIN_DC | defaults to 19 on esp32 and 12 on esp8266 |
| FLD_PIN_RESET | defaults to 26 on esp32 and 16 on esp8266 |
| FLD_TYPE | defaults to SSD1306 or SSD1306_SDI if FLD_SPI_DEFAULT is set |

### four line display alt usermod

| Flag | Description |
| --- | --- |
| FLD_PIN_SCL | defaults to i2c_scl value |
| FLD_PIN_SDA | defaults to i2c_sda value |
| FLD_PIN_CLOCKSPI | defaults to spi_sclk value |
| FLD_PIN_DATASPI | defaults to spi_mosi value |
| FLD_PIN_CS | defaults to spi_cs value |
| FLD_PIN_DC | defaults to 19 on esp32 and 12 on esp8266 |
| FLD_PIN_RESET | defaults to 26 on esp32 and 16 on esp8266 |
| FLD_TYPE | defaults to SSD1306 or SSD1306_SDI if FLD_SPI_DEFAULT is set |

### encoder usermod

| Flag | Description |
| --- | --- |
| ENCODER_DT_PIN | defaults to 12 |
| ENCODER_CLK_PIN | defaults to 14 |
| ENCODER_SW_PIN | defaults to 13 |
| USERMOD_ROTARY_ENCODER_GPIO | defaults to INPUT_PULLUP |

### encoder alt usermod

| Flag | Description |
| --- | --- |
| ENCODER_DT_PIN | defaults to 12 |
| ENCODER_CLK_PIN | defaults to 14 |
| ENCODER_SW_PIN | defaults to 13 |
| USERMOD_ROTARY_ENCODER_GPIO | defaults to INPUT_PULLUP |

### VL53L0X usermod

| Flag | Description |
| --- | --- |
| VL53L0X_MAX_RANGE_MM | max range in millimeters to react for motions, defaults to 230 |
| VL53L0X_MIN_RANGE_OFFSET | minimal range in millimeters that sensor can detect. Used in long motions to correct brightness calculation, defaults to 60 |
| VL53L0X_DELAY_MS | how often to get data from sensor, defaults to 100 |
| VL53L0X_LONG_MOTION_DELAY_MS | switch onto "long motion" action after this delay,defaults to 1000 |
