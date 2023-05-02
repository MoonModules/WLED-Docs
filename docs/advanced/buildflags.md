Buildflags Moon mod  0.14.0-b15.23

####
Disable Features
####
-D WLED_DISABLE_OTA			Disables the feature to Update over the webinterface
-D WLED_DISABLE_ALEXA		Disables Alexa support
-D WLED_DISABLE_HUESYNC		Disables the HUE support
-D WLED_DISABLE_INFRARED	Disables Infrared support
-D WLED_DISABLE_WEBSOCKETS	Disables the websockets (?)
-D WLED_DISABLE_MQTT		Disables MQTT support
-D WLED_DISABLE_SOUND		Disables Sound Features
-D WLED_DISABLE_2D			Disables 2D Features
-D WLED_DISABLE_LOXONE		Disable Loxone Support (?)

###
Audio buildflags
###
-D SR_SQUELCH
-D SR_GAIN
-D AUDIOPIN					Analogaudiopin
-D SR_DMTYPE				0=none/disabled/analog ; 1=generic I2S
-D I2S_SDPIN
-D I2S_WSPIN
-D I2S_CKPIN
-D I2S_USE_16BIT_SAMPLES	If I2S input is already 16 bit
-D ES7243_SDAPIN
-D ES7243_SCLPIN
-D ES7243_ADDR
-D MCLK_PIN
-D SR_DEBUG
-D UM_AUDIOREACTIVE_USE_NEW_FFT
-D MIC_LOGGER
-D FFT_SAMPLING_LOG
-D I2S_USE_RIGHT_CHANNEL
-D I2S_SAMPLE_DOWNSCALE_TO_16BIT





###
Battery usermod
###
-D USERMOD_BATTERY_MEASUREMENT_PIN			Pin to measure the voltage, defaults to GPIO35 on ESP32 and A0 on ESP8266
-D USERMOD_BATTERY_MEASUREMENT_INTERVAL		Interval to measure voltage in ms, defaults to 30s
-D USERMOD_BATTERY_MIN_VOLTAGE				Minimal voltage in volt, defaults to 3.2V if use lipo and min voltage is not set, if min voltage is not set and use lipo is set the dafault is 2.6V
-D USERMOD_BATTERY_USE_LIPO
-D USERMOD_BATTERY_MAX_VOLTAGE				Max voltage in volt, defaults to 4.2V if not set
-D USERMOD_BATTERY_TOTAL_CAPACITY			capacity in mAh defaults to 3100mAh if not set
-D USERMOD_BATTERY_CALIBRATION				offset or calibration value to fine tune the calculated voltage
-D USERMOD_BATTERY_AUTO_OFF_ENABLED			auto-off feature, defaults to true
-D USERMOD_BATTERY_AUTO_OFF_THRESHOLD		Percentage theshold (?)
-D USERMOD_BATTERY_LOW_POWER_INDICATOR_ENABLED	low power indication feature, defaults to true
-D USERMOD_BATTERY_LOW_POWER_INDICATOR_PRESET		defaults to 0
-D USERMOD_BATTERY_LOW_POWER_INDICATOR_THRESHOLD	defaults to 20
-D USERMOD_BATTERY_LOW_POWER_INDICATOR_DURATION		defaults to 5

###
BH1750 usermod
###
-D USERMOD_BH1750_MAX_MEASUREMENT_INTERVAL			the max frequency to check photoresistorin milliseconds, 10 seconds
-D USERMOD_BH1750_MIN_MEASUREMENT_INTERVAL			the min frequency to check photoresistor in milliseconds, 500 ms
-D USERMOD_BH1750_FIRST_MEASUREMENT_AT				how many milliseconds after boot to take first measurement, 10 seconds
-D USERMOD_BH1750_OFFSET_VALUE						only report if differance grater than offset value, default 1

###
BOBlight usermod
###
-D BOB_PORT		Boblight port, defaults to 19333

###
Buzzer usermod
###
-D USERMOD_BUZZER_PIN	Buzzer pin, defaults to GPIO32

###
DHT usermod
###
-D USERMOD_DHT_DHTTYPE					11=DHT 11, 21=DHT 21, 22:DHT 22 (AM2302), AM2321 *** default
-D USERMOD_DHT_MEASUREMENT_INTERVAL		the frequency to check sensorin milliseconds, 1 minute
-D USERMOD_DHT_FIRST_MEASUREMENT_AT		how many seconds after boot to take first measurementin milliseconds, 90 seconds
-D USERMOD_DHT_PIN						defaults to 21 onm ESP32 and 4 on esp8266
-D USERMOD_DHT_MQTT
-D USERMOD_DHT_STATS
-D USERMOD_DHT_CELSIUS

###
BME280 usermod
###
-D Celsius

###
Enclosure usermod
###
-D Celsius

###
MQTTSWITCH usermod
###
-D MQTTSWITCHPINS		define MQTTSWITCHPINSe.g. -D MQTTSWITCHPINS="12, 0, 2"
-D MQTTSWITCHINVERT		invert the switch pins, default all active high
-S MQTTSWITCHDEFAULTS	default behavior, default all off

###
Multi Releay usermod
###
-D MULTI_RELAY_MAX_RELAYS		default to 4
-D MULTI_RELAY_PINS				defaults to -1

###
MY92XX usermod
###
-D DEBUG_MY92XX

###
PIR usermod
###
-D PIR_SENSOR_PIN	defaults to GPIO23 on ESP32 and GPIO13 on ESP8266
-D PIR_SENSOR_OFF_SEC	in milliseconds, defaults to 600ms
-D USERMOD_PIR_SENSOR_SWITCH

###
PWM Fan usermod
###
-D TACHO_PIN	defaults to -1
-D PWM_PIN		defaults to -1

###
PWM OUTPUT usermod
###
-D USERMOD_PWM_OUTPUT_PINS	default to 3

###
Photoresistor usermod
###
-D USERMOD_SN_PHOTORESISTOR_MEASUREMENT_INTERVAL	the frequency to check photoresistor in milliseconds, 10 seconds
-D USERMOD_SN_PHOTORESISTOR_FIRST_MEASUREMENT_AT	how many milliseconds after boot to take first measurement, 10 seconds
-D USERMOD_SN_PHOTORESISTOR_REFERENCE_VOLTAGE		supplied voltage
-D USERMOD_SN_PHOTORESISTOR_ADC_PRECISION			defaults to 1024
-D USERMOD_SN_PHOTORESISTOR_RESISTOR_VALUE			defaults to 10k
-D USERMOD_SN_PHOTORESISTOR_OFFSET_VALUE			only report if differance grater than offset value, defaults to 5

###
SD card usermod
###
-D WLED_USE_SD_MMC
-D WLED_USE_SD_SPI
-D SD_ADAPTER


###
ST7790 usermod
###
-D USER_SETUP_LOADED
-D ST7789_DRIVER
-D TFT_WIDTH
-D TFT_HEIGHT
-D TFT_MOSI
-D TFT_SCLK
-D TFT_DC
-D TFT_RST
-D LOAD_GLCD
-D TFT_BL

###
Stairway whipe usermod
###
-D STAIRCASE_WIPE_OFF

###
Temperature usermod
###
-D TEMPERATURE_PIN									defaults to 18 on ESP32 and 14 on ESP8266
-D USERMOD_DALLASTEMPERATURE_MEASUREMENT_INTERVAL	the frequency to check temperature in milliseconds, 1 minute

###
TTGO TDisplay
###
-D TFT_DISPOFF 		defaults to 0x28
-D TFT_SLPIN		defaults to 0x10

###
autosave usermod
###
-D AUTOSAVE_AFTER_SEC			in seconds, default 15s
-D AUTOSAVE_PRESET_NUM			defaults to 250
-D USERMOD_AUTO_SAVE_ON_BOOT	defaults to false



###
four line display usermod
###
-D FLD_PIN_SCL		defaults to i2c_scl value
-D FLD_PIN_SDA		defaults to i2c_sda value
-D FLD_PIN_CLOCKSPI	defaults to spi_sclk value
-D FLD_PIN_DATASPI	defaults to spi_mosi value
-D FLD_PIN_CS		defaults to spi_cs value
-D FLD_PIN_DC		defaults to 19 on esp32 and 12 on esp8266
-D FLD_PIN_RESET	defaults to 26 on esp32 and 16 on esp8266
-D FLD_TYPE			defaults to SSD1306 or SSD1306_SDI if FLD_SPI_DEFAULT is set

###
four line display alt usermod
###
-D FLD_PIN_SCL		defaults to i2c_scl value
-D FLD_PIN_SDA		defaults to i2c_sda value
-D FLD_PIN_CLOCKSPI	defaults to spi_sclk value
-D FLD_PIN_DATASPI	defaults to spi_mosi value
-D FLD_PIN_CS		defaults to spi_cs value
-D FLD_PIN_DC		defaults to 19 on esp32 and 12 on esp8266
-D FLD_PIN_RESET	defaults to 26 on esp32 and 16 on esp8266
-D FLD_TYPE			defaults to SSD1306 or SSD1306_SDI if FLD_SPI_DEFAULT is set

###
encoder usermod
###
-D ENCODER_DT_PIN 	defaults to 12
-D ENCODER_CLK_PIN 	defaults to 14
-D ENCODER_SW_PIN 	defaults to 13
-D USERMOD_ROTARY_ENCODER_GPIO	defaults to INPUT_PULLUP

###
encoder alt usermod
###
-D ENCODER_DT_PIN 	defaults to 12
-D ENCODER_CLK_PIN 	defaults to 14
-D ENCODER_SW_PIN 	defaults to 13
-D USERMOD_ROTARY_ENCODER_GPIO	defaults to INPUT_PULLUP

###
VL53L0X usermod
###
-D VL53L0X_MAX_RANGE_MM 	max range in millimeters to react for motions, defaults to 230
-D VL53L0X_MIN_RANGE_OFFSET minimal range in millimeters that sensor can detect. Used in long motions to correct brightness calculation, defaults to 60
-D VL53L0X_DELAY_MS 		how often to get data from sensor, defaults to 100
-D VL53L0X_LONG_MOTION_DELAY_MS		switch onto "long motion" action after this delay,defaults to 1000


###
normal WLED buildflags
###
-D WLED_MAX_USERMODS	defaults to 4 on esp8266 and 6 on ESP32
-D WLED_MAX_BUSSES		defaults to 3 on esp8266, 10 on esp32 without AR, 8 on esp32 with AR, 6 on ESP32S3, 6 esp32S2 with AR, 7 on esp32s2 without AR, 3 on ESP32C3
-D WLED_MAX_BUTTONS		defaults to 2 on esp8266 and 4 on esp32
-D WLED_MAX_LEDMAPS		defaults to 10 on esp8266 and 156 on esp32
-D MAX_LEDS				defaults to 1664 on esp8266 and 8192 on esp32
-D MAX_LED_MEMORY		defaults to 4000 on esp8266	and 32000 on esp32C3 and esp32S2, 64000 on ESP32 and ESP32S3
-D MAX_LEDS_PER_BUS		defaults to 2048
-D WLED_USE_ETHERNET	enables Ethernet
-D ABL_MILLIAMPS_DEFAULT	0 to disable minimum is 250, defaults to 850
-D WLED_PWM_FREQ		defaults to 880 on esp8266 and 19531 on esp32
-D LEDPIN				defaults to GPIO2 on esp8266 and GPIO16 on esp32
-D WLED_ENABLE_DMX
-D DEFAULT_LED_COUNT	defaults to 30
-D HW_PIN_SCL			defaults to SCL value
-D HW_PIN_SDA			defaults to SDA value
-D HW_PIN_CLOCKSPI 		defaults to SCK
-D HW_PIN_DATASPI 		defaults to MOSI
-D HW_PIN_MISOSPI 		defaults to MISO
-D WLED_USE_REAL_MATH	use math and not lookuptables
-D DEFAULT_LED_TYPE		defaults to TYPE WS2812_RGB
-D PIXEL_COUNTS			defaults to DEFAULT_LED_COUNT 	!!!!!
-D DATA_PINS			defaults to LEDPIN				!!!!!
-D DEFAULT_LED_COLOR_ORDER	defaults to COL_ORDER_GRB
-D WLED_WATCHDOG_TIMEOUT 	set the whatchdog timout in milliseconds, default to 0 (deactivated)
-D WLED_DISABLE_BROWNOUT_DET
-D CLIENT_SSID
-D CLIENT_PASS
-D WLED_AP_SSID
-D WLED_AP_PASS
-D SPIFFS_EDITOR_AIRCOOOKIE
-D WLED_VERSION	defaults to "dev"
-D BTNPIN
-D RLYPIN
-D RLYMDE	1=active high, 0= active low
-D IRPIN
-D SERVERNAME	defaults to "WLED"
-D WLED_DEBUG_HOST
-D WLED_DEBUG_PORT	defaults to 7868
-D WLED_AP_SSID_UNIQUE
-D WLED_DEBUG
-D LED_BUILTIN
-D WLED_USE_IC_CCT
-D WLED_MAX_CCT_BLEND
-D WLED_ADD_EEPROM_SUPPORT
-D ESP32_DATA_IDLE_HIGH
-D WLED_ENABLE_SIMPLE_UI
-D WLED_ENABLE_MQTT
-D WLED_ENABLE_JSONLIVE
-D WLED_DEBUG_FS
-D WLED_DEBUG_IMPROV
-D WLED_ENABLE_LOXONE
-D WLED_ENABLE_WEBSOCETS
-D WLED_ENABLE_ADALIGHT
-D WLED_DEBUG_NTP
-D WLED_USE_PSRAM
-D WLED_ENABLE_PIXART





###
USERMODS
###
-D USERMOD_BATTERY				usermod_v2_Battery.h
-D USERMOD_DALLASTEMPERATURE	usermod_temperature.h
-D USERMOD_SHT					usermod_sht.h
-D USERMOD_SN_PHOTORESISTOR		usermod_sn_photoresistor.h
-D USERMOD_PWM_FAN				usermod_PWM_fan.h
-D USERMOD_BUZZER				usermod_v2_buzzer.h
-D USERMOD_SENSORSTOMQTT		usermod_v2_SensorsToMqtt.h
-D USERMOD_PIRSWITCH			usermod_PIR_sensor_switch.h
-D USERMOD_MODE_SORT			usermod_v2_mode_sort.h
-D USERMOD_BH1750				usermod_BH1750.h
-D USERMOD_BME280				usermod_bme280.h
-D USERMOD_FOUR_LINE_DISPLAY	usermod_v2_four_line_display.h
-D USERMOD_ROTARY_ENCODER_UI	usermod_v2_rotary_encoder_ui.h
-D USE_ALT_DISPlAY				Alt versions of the two above instead of normal
-D USERMOD_AUTO_SAVE			usermod_v2_auto_save.h
-D USERMOD_DHT					usermod_dht.h
-D USERMOD_VL53L0X_GESTURES		usermod_vl53l0x_gestures.h
-D USERMOD_ANIMATED_STAIRCASE	Animated_Staircase.h
-D USERMOD_MULTI_RELAY			usermod_multi_relay.h
-D USERMOD_RTC					usermod_rtc.h
-D USERMOD_ELEKSTUBE_IPS		usermod_elekstube_ips.h
-D USERMOD_ROTARY_ENCODER_BRIGHTNESS_COLOR	usermod_rotary_brightness_color.h
-D RGB_ROTARY_ENCODER			rgb-rotary-encoder.h
-D USERMOD_ST7789_DISPLAY		ST7789_Display.h
-D USERMOD_SEVEN_SEGMENT		usermod_v2_seven_segment_display.h
-D USERMOD_SSDR					usermod_seven_segment_reloaded.h
-D USERMOD_CRONIXIE				usermod_cronixie.h
-D QUINLED_AN_PENTA				quinled-an-penta.h
-D USERMOD_WIZLIGHTS			wizlights.h
-D USERMOD_WORDCLOCK			usermod_v2_word_clock.h
-D USERMOD_MY9291				usermode_MY9291.h
-D USERMOD_SI7021_MQTT_HA		usermod_si7021_mqtt_ha.h
-D USERMOD_SMARTNEST			usermod_smartnest.h
-D USERMOD_AUDIOREACTIVE		audio_reactive.h
-D USERMOD_ANALOG_CLOCK			Analog_Clock.h
-D USERMOD_PING_PONG_CLOCK		usermod_v2_ping_pong_clock.h
-D USERMOD_ADS1115				usermod_ads1115.h
-D USERMOD_BOBLIGHT				boblight.h
-D USERMOD_PWM_OUTPUTS			usermod_pwm_outputs.h
-D SD_ADAPTER					
-D USERMOD_KLIPPER_PERCENTAGE	usermod_v2_klipper_percentage.h





###
MM special
###

###
Artifx
###
-D ARTI_DEBUG
-D ARTI_ANDBG
-D ARTI_RUNLOG
-D ARTI_PRINT
-D ARTI_ERRORWARNING
-D ARTI_MEMORY
-D OPTIMIZED_TREE

###
Pinmanager
###
-D SOC_ADC_CHANNEL_NUM
-D MPU6050_INT_GPIO

###
internal
###
-D WLED_DEBUG_MATH

###
USERMODS
###
-D USERMOD_MPU6050_IMU
-D ARTIFX
-D WEATHER
-D USERMOD_GAMES
-D USERMOD_FASTLED
