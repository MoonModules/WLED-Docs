---
title: Release notes v0.14.0-b3-daily
hide:
  # - navigation
  # - toc
---

Below are the ongoing updates in WLEDMM which has not made it to a release yet (Next major release will be v0.14.1-b30)

# MoonModules v0.14.3-b32 (work in progress)


## Info Page improvements

May 4th

System information in the "Info" panel re-organized, and PSRAM statistics added.

<img width="65%" alt="new INFO Panel" src="https://github.com/MoonModules/WLED-Docs/assets/91616163/7160bf79-3f27-42e7-8ef1-9c6fc930b983">


by By @softhack007

## Lots of bugfix back-porting from upstream

ongoing, 2024

Due to technical incompatibilities to latest upstream source code, WLEDMM is still building on the WLED core from summer 2023 (long story...). We have however made an effort to analyze bugfixes from upstream until version 0.14.3, and brought them into WLED-MM if possible. We also pack-ported a few features from upstream 0.15.0-beta.

by @softhack007


## Updated DMX Input - now with RDM support

Feb 10th, 2024

The (wired) DMX Input has been given significant rewrite by @arneboe and now supports RDM - NOTE: you will need to re-enter all 3 pins used when you upgrade to this version

## gamma-correct palettes preview

Jan 25th, 2024

old
<img width="40%" alt="old preview" src="https://github.com/MoonModules/WLED-Docs/assets/91616163/388e9b89-2ada-400e-8db9-270a7d965f2f">
  &nbsp; new 
<img width="40%" alt="new preview" src="https://github.com/MoonModules/WLED-Docs/assets/91616163/2911ac6a-5f0d-4622-b7eb-941f0ee67070">

# MoonModules v0.14.1-b30

By @softhack007

## option to disable sequence checking in sound sync

Jan 5th, 2024

UDP sound sync - sequence checking can be disabled in settings (useful if several units send sound)

![Screenshot_20240129-225644](https://github.com/MoonModules/WLED-Docs/assets/91616163/caa60c45-0c37-4441-96a4-b5e55db930f0)


By @softhack007

## new audio reactive effects (enhancing standard effects)

Dec 31st, 2023 

Audio Reactive standard effects - 
clap your hands - Popcorn ;-)

![20240129_225228](https://github.com/MoonModules/WLED-Docs/assets/91616163/e415834e-2876-4f51-adef-fa51315bc6f4)

 back-ported from WLED-SR. These "audio enhanced" effects are triggered by sound. Like clapping of hands, music starts, beats, fireworks explosions.

The popcorn audio effect looks particularly great in 2D mode - select 1D-2D mapping "bars").

By @softhack007


## build runs-anywhere usermods

Dec 15th, 2023

WLEDMM now allows you to encapsulate your MoonModules specific code like this:

```C++
class ShtUsermod : public Usermod
{
  private:
#ifndef _MoonModules_WLED_
    bool enabled = false; // Is usermod enabled or not //WLEDMM not needed - using public attribute of class UserMod
#endif

  public:
#ifdef _MoonModules_WLED_
    ShtUsermod(const char *name, bool enabled):Usermod(name, enabled) {} //WLEDMM usermod initializer with parameters
#endif

void ShtUsermod::setup()
{
  if (enabled) {

#ifdef _MoonModules_WLED_
    if ((i2c_sda >= 0) && (i2c_scl >= 0) && pinManager.joinWire(i2c_sda, i2c_scl)) {   // WLEDMM pin management done by pinManager.joinWire()
      pinAllocDone = true;
    } else {
      USER_PRINTF("[%s] SHT pin allocation failed!\n", _name);                       // WLEDMM using USER_PRINTF for important messages
      cleanup();
      return;
    }
#else
    PinManagerPinType pins[2] = { { i2c_sda, true }, { i2c_scl, true } };
    if (i2c_sda < 0 || i2c_scl < 0 || !pinManager.allocateMultiplePins(pins, 2, PinOwner::HW_I2C)) {	
      DEBUG_PRINTF("[%s] SHT pin allocation failed!\n", _name);
      cleanup();
      return;
    } else pinAllocDone = true;
#endif
  }
  initDone = true;
}

```

By @softhack007

## UDP Sound Sync improvements

December 2023

###  Latency reduced drasticially
Latency from microphone to receiving sound on the remode unit has been optimized drasticially.
Previously the average delay was 30-60ms. With our optimized code, UDP packets are sent out directly when new samples arrive from the driver, resulting in average delay of 10-25ms.

By @softhack007

### New UDP sync mode "Receive or Local"
Acts like "Receive", however automaticially falls back to local whenever the UDP stream is missing.

![image](https://github.com/MoonModules/WLED-Docs/assets/91616163/dd74010b-7904-463c-8f7c-e9668f8046cd)

![image](https://github.com/MoonModules/WLED-Docs/assets/91616163/cff0a14b-629f-4967-b2e4-8f5db5b66387) 
 Local input when sender is missing.

![image](https://github.com/MoonModules/WLED-Docs/assets/91616163/5c4728c1-8fb5-4f4b-b930-760cc2276802) 
 Automatic switch-over to network sound.


By @softhack007

### UDP sound sequence checking (framecounter)
UDP transport itself does neither guarantee delivery nor sequence.

Leveraging on a previously unused byte in the UDP sound sync format, 
WLED-MM now checks that a newly received sound sample is "in sequence". 
Too-late packets will be dropped, leading to smoother animations.

By @netmindz


## Presets name and default checkboxes

Nov 23st, 2023

<video width="400" autoplay><source src="https://github.com/MoonModules/WLED-Docs/assets/138451817/1bb0d7a9-3724-47c6-99e1-a8b341c52d05" type="video/mp4"></video>

Default name of new preset now includes the icons (cause it's nice to know if a preset is sound reactive or not)
Preset checkboxes have now default of last set values (cause it's handy of you don't want to save brightness it is not saved in next preset save as well)

By @ewowi

## Super Sync

October 15, 2023
By @ewowi

Super Sync runs one effect on multiple instances allowing for higher framerates as each instance runs only part of the effect.

![image](https://github.com/MoonModules/WLED-Docs/assets/91013628/37005643-b39b-4764-bfab-774461585d1c)

The nodes tab shows more info per instance, info which is needed for SuperSync.

SuperSync takes all the panels in the 2D config setup and each panel will be setup on a different node. 

* Master node is in red
* Orange: non critical differences with the master node
* Red: client node is not setup right

* SuperSync button: for all nodes with a red yes in the SSync column the desired configuration will be send and configured on that node. After pressing SuperSync all nodes should be in the right config

* SuperSync is work in progress. Some effects run perfect, others not yet. This has mostly to do with the random function giving different values on different instances. Some effects have been adapted to give the same values for random using the same random seeds

Example of setup of supersync on 3x3 = 9 nodes:

<video width="400" autoplay><source src="https://github.com/MoonModules/WLED-Docs/assets/91013628/11a463eb-b8da-4d09-80ad-dc4219075cd2" type="video/mp4"></video>


## WM8978 support for Ohmic Pico DSP

Oct 20st, 2023

Essentially a similar type of chip to the ES8388 - I2S codec configured over I2C. Configured for line-in with pass-thru on the Ohmic ESP32 Pico D4 DSP board: https://github.com/ohmic-net/puca_dsp

May not work out of the box with all WM8978 boards because of the vast configuration options in the codec, but could easily be adjusted for various configurations. Not that there's many out there. :)

By @troyhacks


## Lots of bugfix back-porting from upstream

Dec 16th, 2023

Due to technical incompatibilities to latest upstream source code, WLEDMM is still building on the WLED core from summer 2023 (long story...).
We have however made an effort to analyze bugfixes from upstream until version 0.14.1-beta, and brought them into WLED-MM if possible.

As a user, you get our latest features, combined with various stability improvements and bugfixing made in upstream WLED. 
Plus all bugfixing and improvements of MM specific features that were created in the last 3 months.

by @softhack007


