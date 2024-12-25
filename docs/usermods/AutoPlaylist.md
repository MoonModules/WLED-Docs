---
title: Usermod Auto Playlist
hide:
  # - navigation
  # - toc
---

## Auto Playlist

v2 Usermod to automatically change between two playlists:

* A playlist for when music/audio is present (MusicPlaylist)
* A playlist for when silence is present (AmbientPlaylist)

Optionally, "AutoChange" will advance your music playlist automatically when the musicality suggests a good time to change presets.

**Note**: _The playlist you have designated as "MusicPlaylist" must be active for the AutoPlaylist function to take control of your presets._

### Settings

* **Enabled** - Enables/disables the usermod.
* **Timeout** - Sets the amount of silence needed before a change to AmbientPlaylist.
* **AmbientPlaylist** - The playlist ID (number) of your ambient playlist.
* **MusicPlaylist** - The playlist ID (number) of your music/audio-detected playlist.
* **AutoChange** - Enables/disables automatic changing of presets in your MusicPlaylist based on musicality.
* **Change Lockout** - If AutoChange is enabled, don't ever change more than this number of milliseconds. Strictly enforced.
* **Ideal Change Min** - Sets the ideal fastest change you want in milliseconds. Not strictly enforced.
* **Ideal Change Max** - Sets the ideal slowest change you want in milliseconds. Not strictly enforced.

### AutoChange

AutoChange looks at the properties of the incoming audio to try and determine a good time to change presets in your music playlist.

This is entirely just "for fun" and should not to be relied on to be overly accurate, etc. It's a calculation, not a VJ or lighting artist - but it does a reasonable job.

AutoChange works with some new values computed in the AudioReactive usermod:

* **zeroCrossingCount** - The number of times the incoming sound crosses the zero line of the waveform
* **energy** - The squared prodict of adding up all the calculated and normalized FFT results
* **lowFreqencyContent** - Currently just the lowest bin of the calculated and normalized FFT results.

These values are each calculted as two averages in the AutoPlaylist usermod:

* A fast-moving average for each of the 3 values
* A slow-moving average for each of the 3 values

Finally, a vector is computed to determine the difference between the two average pools. When this vector is minimal, the preset is changed.

The change threshhold is calculated on the fly and adjusted up or down based on if we are faster or slower than our ideal change window.

"Change Lockout" will prevent the usermod from changing the presets more frequently than this number of milliseconds, 
but "Ideal Change Min" and "Ideal Change Max" simply influence the calculated change threshold. If the calculated vector 
is lower than the current change threshold AND change lockout has been exceeded, a preset change will almost **always** take place (see note).

* **NEW:** A change between change_lockout and change_lockout+3ms is now skipped to prevent "freefall" changes.

When a change happens more quickly than "Ideal Change Min" or more slowly than "Ideal Change Max", the change threshold is 
adjusted accordingly.

If we haven't seen a change by the time "Ideal Change Min" has occured, the change threshold is increased to the minimum distance detected to
increase the chances of detecting a change happening within the time window. This also helps AutoChange adjust to different music over time, 
like when a track changes. 

### Installation

Add this to `build_flags` in your platformio_override.ini file:

  `-D USERMOD_AUTO_PLAYLIST`

Optionally you can add this to enable the usermod's specific debug output:

  `-D USERMOD_AUTO_PLAYLIST_DEBUG`

This debug is also automatically enabled with `-D WLED_DEBUG` as well.

#### PlatformIO requirements

No special requirements.

### Change Log

2024-12-25

This document: Some typos fixed, clarifications added, formatting fixed. 

2024-04-04

* Docs updated with debug flag. 

2024-03-25

* Pre-Beta release, docs added.
  


