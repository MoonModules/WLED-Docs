Q. Is it possible to use my PC for the sound and without using the microphone, or any ADC pins on the board.

The sound reactive fork of WLED was designed as an all-in-one unit that doesn't require the intervention of a PC. You can setup a display and have it run completely independently. It supports your PC's analog line-out signal, several analog microphones, an INMP441 digital microphone, as well as UDP sound sync:

<https://mm.kno.wled.ge/WLEDSR/UDP-Sound-Sync>

To answer this question, there is not a direct, built in way, except for the line-out signal.
Although we support UDP sound sync, someone would have to write a program for their OS of choice to capture the sound from the PC, perform FFT calculations, and UDP transmit the sampled data (the packet matching our sound reactive WLED data structure). That's a non-trivial course of action.

All that being said, there are a couple ways to achieve this:

For windows, there is **WledSRServer** (<https://github.com/Victoare/SR-WLED-audio-server-win>) which is a small application that is using the mentioned sound capture, FFT calculation and UDP packet sending mechanism.

There is also **LedFx** (as found at <https://github.com/LedFx/LedFx>) which is an another solution for this use case with a different approach. Since WLED supports UDP, DDP, and E1.31 DMX protocols, you can use the sound reactive LedFx running on your PC to control a WLED device. There's an excellent video on setting this environment up at <https://www.youtube.com/watch?v=ipSfQdfX4fE>.

LedFx will then directly control the LED's on your WLED device, although you can still revert to native WLED animations.
