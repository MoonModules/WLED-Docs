tha ---
title: Release notes v0.14.0-b3-daily
hide:
  # - navigation
  # - toc
---

Below are the ongoing updates in WLEDMM which has not made it to a release yet (Next release will be v0.14.0-b2)

## Some `_S` builds are optimized for speed

July 21st, 2023

By @Softhack007

Some MoonModules builds are now utilizing compiler option -O2 "optimize for speed", instead of -Os "optimize for size".

As the firmware size grows with this option, only a few `_S` firmware binaries for esp32 are currently build with this higher optimization level:

* `esp32_4MB_S` (flash usage 87.4% --> 98.8%)
* `esp32_16MB_V4_S` (flash usage 73.3% --> 82.9%)
* `esp32_16MB_S` (includes animartix)
* `esp32S3_8MB_S` for -S3 (up to 45% faster than normal build!)


First tests show 20%-35% higher FPS (framerates) in effects!



Known issue: USERMOD_ANIMARTRIX aborts with internal compiler error when building with `-O2`:
```
wled00/../usermods/usermod_v2_animartrix/usermod_v2_animartrix.h: In function 'uint16_t mode_Waves()':
wled00/../usermods/usermod_v2_animartrix/usermod_v2_animartrix.h:340:1: error: insn does not satisfy its constraints:
 }
 ^
 (insn 811 738 824 24 (set (reg/v:SF 19 f0 [orig:69 result ] [69])
        (mem/u/c:SF (symbol_ref/u:SI ("*.LC1575") [flags 0x2]) [0  S4 A32])) ".pio/libdeps/my_esp32_16MB_V4_S_debug/animartrix/ANIMartRIX.h":345 47 {movsf_internal}
     (nil))
 during RTL pass: postreload
 wled00/../usermods/usermod_v2_animartrix/usermod_v2_animartrix.h:340:1: internal compiler error: in extract_constrain_insn, at recog.c:2210
 libbacktrace could not find executable to open
 Please submit a full bug report, with preprocessed source if appropriate. See <https://gcc.gnu.org/bugs/> for instructions.
```


## Topic

Date

By @Netmindz

