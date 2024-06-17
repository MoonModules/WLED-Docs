---
title: Sound Sync
hide:
  # - navigation
  # - toc
---
# Sound Sync

If you have more than one device or wish to use [Line Input](Line-Input) but your audio source is not right next where your LEDs are, then Audio Sync is the feature you need, no need for multiple mics or long cables. Sound Sync is different from direct LEDs control using protocols like E1.31, DMX, DDP or AdaLight.

For the WLED instance that you wish to be the source, simply set the Sync mode in the Audio Reactive module to Send and then use Recieve on all the WLED instances you wish to use the data

You might have a setup something like this or just a simple wired line-in rather than Bluetooth or Chromecast

<img src="https://media.discordapp.net/attachments/853969074311659570/1120723508717158510/WLED_Audio_Routing_Diagram.png"/>

UDP Sound Sync is a feature to synchronize (share) the sound input of a 'master' device with one or more 'slave' devices. 

UDP Sound Sync does not sync the actual animations, but rather transmits summary audio sampling information to several devices that still run their own animations locally. In a nutshell, it means that several devices can share a single audio source.

## Setup
Before configuring UDP Sound Sync, make sure you have gone into the WiFi Preferences and clicked on 'Disable WiFi sleep' at the bottom of the page. It has caused us innumerable problems in the past.

In order to configure UDP sound sync, the ‘master’ needs to be an ESP32 configured as normal, but with Sync Mode set to Send

For devices without an audio input, Audio Reactive must be enabled but with the Sync Mode set to Receive. Make sure the UDP port is the same on all devices.

In order to change the UDP Sync Mode (Disabled/Transmit/Receive), you need to power-cycle the ESP32.

## Technical

When an ESP32 is configured for audio transmission, it will connect to a UDP Multicast address, and begin sending a single UDP Multicast packet containing the data used to generate sound-reactive animations out to any other devices that are configured to receive on the same network.  The following information is transmitted:

### V1 format, used in SR WLED up to 0.13.x
```c++
#define UDP_SYNC_HEADER "00001"
struct audioSyncPacket {
  char header[6] = UDP_SYNC_HEADER;
  uint8_t myVals[32];     //  32 Bytes
  int sampleAgc;          //  04 Bytes
  int sampleRaw;          //  04 Bytes
  float sampleAvg;        //  04 Bytes
  bool samplePeak;        //  01 Bytes
  uint8_t fftResult[16];  //  16 Bytes - FFT results, one byte per GEQ channel
  double FFT_Magnitude;   //  08 Bytes
  double FFT_MajorPeak;   //  08 Bytes
};
```

UDP_SYNC_HEADER is a versioning number that's defined in audio_reactive.h

### V2 Format - WLED version >= 0.14.0 (including MoonModules fork)

```c++
#define UDP_SYNC_HEADER_V2 "00002"

// new "V2" audiosync struct - 44 Bytes
    struct __attribute__ ((packed)) audioSyncPacket {  // WLEDMM "packed" ensures that there are no additional gaps
      char    header[6];      //  06 Bytes  offset 0
      uint8_t gap1[2];        // gap added by compiler: 02 Bytes, offset 6
      float   sampleRaw;      //  04 Bytes  offset 8  - either "sampleRaw" or "rawSampleAgc" depending on soundAgc setting
      float   sampleSmth;     //  04 Bytes  offset 12 - either "sampleAvg" or "sampleAgc" depending on soundAgc setting
      uint8_t samplePeak;     //  01 Bytes  offset 16 - 0 no peak; >=1 peak detected. In future, this will also provide peak Magnitude
      uint8_t frameCounter;   //  01 Bytes  offset 17 - track duplicate/out of order packets
      uint8_t fftResult[16];  //  16 Bytes  offset 18
      uint8_t gap2[2];            // gap added by the compiler: 02 Bytes, offset 34
      float  FFT_Magnitude;   //  04 Bytes  offset 36
      float  FFT_MajorPeak;   //  04 Bytes  offset 40
    };

```

The V2 format expects that AGC is performed by the sender, so there is no need to transmit "AGC" and "non-AGC" samples separately. To save bandwidth, the `myvals[]` array was removed, and all numbers are either `float` or `uint8_t`.

SR-WLED 0.13.3 still sends out V1 format, however it is able to receive and decode V2 format, too.

## values

* In general, all sample data is scaled to be in the range of [0...255], to make effects happy. For the values transmitted as `float`, additional accuracy can be provided by using the fraction part of the number - for example `sampleSmth= 127.125`. Samples transmitted  are the max value from approx 20 milliseconds of sampling, with AGC gain already applied.
* fftResult[16] are [16 frequency "channels"](https://github.com/MoonModules/WLED/blob/fc173b3bc00694e59b653ca230133052b5476c05/usermods/audioreactive/audio_reactive.h#L733-L760), values in the range of [0...255]
* uint8_t samplePeak: 0 if no peak, 1 if peak
* FFT_MajorPeak: strongest frequency from the FFT analysis, in Hz. Minimum frequency is 40hz.
* FFT_Magnitude: amplitude of the strongest frequency- in units that only the ArduinoFFT library knows 🤷 . Typical range is [0... 4096].


## What else ?

You might want to take a look at [this](https://github.com/netmindz/WLED-sync) library, which allows to [send and receive WLED Audio Sync data](https://github.com/netmindz/WLED-sync) independent from WLED.


When configured to receive audio data from another device, the receiver will *disable* any onboard microphone sampling and FFT processing, in favor of audio data received from the network.  Any time a UDP Multicast packet is received from a transmitter, it will be treated as a discrete microphone sample and stored in memory the same way it would be if it were a local microphone.

* The UDP &nbsp;<em>Multicast</em>&nbsp; IP is `239.0.0.1`, and the default UDP port is `11988`.
* The software sends/receives one packet every 20 milliseconds (approx). An external sender may be slower, but not faster than 20ms = 50fps.
* UDP port can be changed in WLED config pages, for example to have several groups of devices by assigning different UDP ports to each group.
* UDP multicast can sometimes have issues with some Wifi routers, if you have issues, please try with a different Wifi

## Using a PC as source (PC audio to WLED)

For windows, there is **WledSRServer** (<https://github.com/Victoare/SR-WLED-audio-server-win>) which is a small application that is doing the audio capturing, FFT computation and packet sending on the system. It sends out V2 packets.



UDP Sound sync brought to you by @spedione on Discord.
