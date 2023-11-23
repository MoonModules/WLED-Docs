---
title: Human Sized Cube
hide:
  # - navigation
  # - toc
---

## Hardware

![image](https://github.com/MoonModules/WLED-Docs/assets/138451817/8ef936f1-434b-46bc-a523-ced7400e2f12)

* Black numbers: GPIO pins (can be replaced by another set of pins)
* Red numbers: Panels: 1..4 are the side panels, 5 is the top panel

## Software

* Use WLED MM latest
* _S is in theory the most stable but _M works fine as well
* Tested with wemos_shield_esp32_16MB_S and wemos_shield_esp32_16MB_M

### Led configuration

<img width="321" alt="image" src="https://github.com/MoonModules/WLED-Docs/assets/138451817/5e8facc5-1df7-4c5a-a50f-20edef02b024">

* With unlimited brightness estimated current is 15A
* When using Serg74 Wemos shield max current of 10A should be used. In practice brightness is about the same

<img width="244" alt="image" src="https://github.com/MoonModules/WLED-Docs/assets/138451817/13b515ea-71bd-49bd-b53e-37ecc0a4a7c7">

* Match the gpio pins with the sides / pins in above image
* Note: Panel numbering starts at 1

<img width="150" alt="image" src="https://github.com/MoonModules/WLED-Docs/assets/138451817/e810ef75-ede2-4639-a18f-d20a8b27f837">

* Uncheck global led buffer, although it should work, this is the main reason for crashes. If unchecked VERY stable.

### 2D setup

<img width="348" alt="image" src="https://github.com/MoonModules/WLED-Docs/assets/138451817/5a8334cd-ab32-4f22-a4ea-eca552c90edc">

* Setup as 5 horizontal panels (advanced setup) so of no ledmap is used, effects run smooth on the sides (top is the 5th panel)

* First two panels start top right, rest top left, see above image

* Note: Panel numbering starts at 0

## Config, presets and ledmaps

* Can be found here: https://github.com/MoonModules/WLED-Effects/tree/master/Ledmaps/Cube20205

* cfg.json can be used to create above setup

* presets.json contains a set of well tested presets

* ledmap1.json and ledmap2.json are used in effects

* import using <ip>/edit

## Fork specific info

| Feature | [WLED SR 0.13](https://github.com/atuline/WLED/tree/dev) | [MoonModules WLED 0.14](https://github.com/MoonModules/WLED/tree/mdev) | [Upstream WLED 0.14](https://github.com/Aircoookie/WLED) |
|---|---|---|---|
Ledmaps|Yes|Yes|Yes

