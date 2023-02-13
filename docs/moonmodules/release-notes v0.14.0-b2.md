---
title: Release notes v0.14.0-b2
hide:
  # - navigation
  # - toc
---

Version b2 has not been official released yet so this is work in progress

## Pin drop downs support read only and reserved pins
January 14, 2023

<img width="144" alt="Screenshot 2023-01-14 at 18 42 14" src="https://user-images.githubusercontent.com/91013628/212558236-50c7da14-6e7c-489e-bc43-778979e9f844.png">

For more information see https://mm.kno.wled.ge/usermods/globalpins/
This page is shown if you press here: 

<img width="200" src="https://user-images.githubusercontent.com/91013628/212558383-fa3f4171-fda7-4d02-b749-bfff03226952.jpeg">

## Generate presets and playlists
January 12, 2023

Generate presets of all effects and group them together in playlists for 1D or 2D, Volume or FFT, combinations or all

<video width="160" autoplay><source src="https://user-images.githubusercontent.com/91013628/212558544-1c42abef-9567-4431-b940-366b7ce3362f.mov" type="video/mp4"></video>

<img width="221" alt="Screenshot 2023-01-13 at 15 29 50" src="https://user-images.githubusercontent.com/91013628/212558671-08aa50bd-4cef-4103-85bc-aeb8b37f8aa6.png">

## I2C and SPI pins make over
Januari 9, 2023

We were not happy how currently pins are managed. It raises questions in discord we could not answer so we decided to refactor it. It's not easy as a lot is interconnected but we made the first steps:

* Drop down for pin variables (see below)
* Rebuild the usermods (pins) settings screen so it works the same
* create _all bin files with a lot of usermods in it so we can test and improve
* do not reset ui variables if something is wrong (e.g. 4ld/type, enabled)
* use errorMessage instead and show errormessage in settings ui
* if global pins are -1, then there is no initialization of spi/i2c if usermods set pins to use global no initialisation
* HLD_PIN_* variables are used in platformio to specify defaults for global pins, no use of the recent introduced new variables I2CSDAPIN (etc) as causes more confusion, HLD_PIN serve these function and is used instead, 
* HW_PIN_DATASPI and HW_PIN_MOSISPI both existed but is one pin, merged to HW_PIN_MOSISPI as MOSI and MISO is both data
* i2c_scl (etc) variables are used in usermods without if -1 then HLD_PIN check, i2c_scl (etc) most be proper initialized before it can be used.
* No hijacking of global vars (giving them a value) in usermods 
* Don't register pins if usermod is not enabled
* create pinManager.joinWire and use as simplified way in usermods

This will be work in progress the coming weeks to implement in usermods (AudioReactive and 4LD working, others likely working but must be tested)

Overview of usermods available in _all bins:

<img width="224" alt="Screenshot 2023-01-08 at 15 13 00" src="https://user-images.githubusercontent.com/91013628/211351663-28e23710-b8e5-441b-8ec3-ff774b0dd106.png">


