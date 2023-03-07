---
title: Release notes v0.14.0-b2-daily
hide:
  # - navigation
  # - toc
---

Below are the ongoing updates which has not made it to a release yet (Next release will be v0.14.0-b2)

## GEQ Smooth Bars
7 March 2023

New option to the GEQ effect: smooth bars. It's intended for matrices with >24 columns, where you would see a "staircase" effect because we only have 16 frequency channels. With the new option enabled, it looks like more channels are availeable and stairs are smoothed out.

<img width="275" alt="image" src="https://user-images.githubusercontent.com/91013628/223497924-955b42ee-d3f3-49de-bd44-45461f80bc01.png">

<video width="350" autoplay><source src="https://user-images.githubusercontent.com/91013628/223497688-44ec61ff-ca7d-46fa-ac68-b3cf71f0e7f2.mov" type="video/mp4"></video>

## Ledmap properties
1 March 2023

<img width="222" alt="image" src="https://user-images.githubusercontent.com/91013628/223077405-2c37bec0-3d94-4ff8-9725-fdfca886f559.png">

See [Advanced/Mapping/0.14 MM](https://mm.kno.wled.ge/advanced/mapping/#014-mm)

Example:

<video width="350" autoplay><source src="https://user-images.githubusercontent.com/91013628/223500900-33834029-28c6-4872-9018-141d7db684e2.mov" type="video/mp4"></video>

## Manage NetDebug / Serial logging in settings 
24 Februari 2023

No need to specify ip address and port in platformio.ini and therefor hardcode in bin/esp32. Go to Sync Interfaces / Net debug and specify there. Set output to network pressing Net Debug in the info tab (default off after reboot).

<img width="400" alt="image" src="https://user-images.githubusercontent.com/91013628/221207210-dabf4dae-efd5-4c76-9c35-2629d9d88fa8.png">

<img width="271" alt="image" src="https://user-images.githubusercontent.com/91013628/221207063-36e19f97-c6a8-44dd-be83-866dce3d8715.png">

<video width="500" autoplay><source src="https://user-images.githubusercontent.com/91013628/221207891-dd302ef2-853d-45b0-92d8-4c144761cbe2.mov" type="video/mp4"></video>

Bins WLEDMM_0.14.0-b2.19_esp32_4MB_M_debug and WLEDMM_0.14.0-b2.19_esp32_16MB_M_debug have NetDebug enabled by default.

To do: check if NetDebug can be enabled in all bins (without performance/network consequences), also when WLED_DEBUG is off to catch Serial output.

## 2D Ledmaps
* segment names
* default ledmaps
* show in segments
* persistant storage
* No reboot necessary if upload new ledmaps

<video width="500" autoplay><source src="https://user-images.githubusercontent.com/1737159/218800190-8bf2a4a2-d058-4560-9bbd-157fbc746716.mov" type="video/mp4"></video>

<img width="500" alt="Screenshot 2023-02-14 at 13 04 01" src="https://user-images.githubusercontent.com/1737159/218801422-8dde6896-9f00-4b6e-84c3-5f1692cdb190.png">

## Segment visualization
* support mirror, reverse, transpose
* support grouping and spacing
* multi segment support

<img width="287" alt="Screenshot 2023-02-07 at 10 18 53" src="https://user-images.githubusercontent.com/1737159/218798487-34701396-0542-4865-9fae-e792582104e6.png"><img width="255" alt="Screenshot 2023-02-06 at 16 14 56" src="https://user-images.githubusercontent.com/1737159/218798950-3e36ab5c-85f6-4469-924a-91fbd9227709.png">

## 2D setup: basic and advanced

<video width="320" autoplay><source src="https://user-images.githubusercontent.com/1737159/218800542-0f8bb19e-4cd8-43ec-8c52-40b41a3b3b05.mov" type="video/mp4"></video>

## 2D setup: Panel visualization
* Reset segments only bounds, keep effect etc.

## Grandient Random cycle palette

<img width="257" alt="image" src="https://user-images.githubusercontent.com/1737159/218804182-8f30b1d9-42fb-4f25-b76a-ad4e4eb7ab08.png">

## Pins
* default pins -1
* Analog pins in dropdown
* D0-D8, RX, TX info in dropdowns
* Any gpio on 8266

## Audio reactive optimizations

## Generate presets

<video width="320" autoplay><source src="https://user-images.githubusercontent.com/1737159/218799772-930c87f1-4abf-403e-8ed7-899008d23dba.mov" type="video/mp4"></video>

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


