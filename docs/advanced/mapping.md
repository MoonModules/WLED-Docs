---
title: Mapping
hide:
  # - navigation
  # - toc
---

WLED now has the ability to remap your LED strip programmatically.

### What is it?
This allows us to treat the WLED strip as if it is wired in any way - we can then use the mapping feature to address the strip in any order. This allows for matrix support, serpentine runs and such.

### How do we do it?

Navigate to the edit page for your WLED device by adding `/edit` to its' address - for example, https://my-led-device.local/edit
Use this edit page to create a file called `ledmap.json`.

`ledmap.json` file needs to be a JSON formatted file with the the key being "map" and the value being an array of numbers representing the new order of pixels. The _position_ of values in the array is the "natural" order of LEDs and the value entered is the new position.
  
The ArduinoJSON library is *****extremely***** white-space sensitive.
If your `ledmap.json` file is not working, check for white-spaces where they should not be. The LED positions are zero-indexed.

Multiple maps are supported in the latest versions by using `ledmapx.json` where x is a number. Maps can be selected in a preset using `{"ledmap":x,...`.

Use -1 in the map for gaps/blank/nul LEDs.

### Examples 
In the below example (formatted multiple ways), we remap a strip of four LEDs from a physical order of 0 1 2 3 into a new order of 0 2 1 3.

    {"map":[0,2,1,3]}

    {"map":[
    0,2,1,3
    ]}

    {"map":[
    0,2,
    1,3
    ]}


This is another example that switches direction every 5 LEDs.
It could be formatted any of the three ways demonstrated above.
  
```json
{"map":[0, 1, 2, 3, 4, 9, 8, 7, 6, 5, 10, 11, 12, 13, 14,
19, 18, 17, 16, 15, 20, 21, 22, 23, 24, 29, 28, 27, 26, 25]}
```

### 0.14 AC
* In 2D, physical mapping of map coordinates to panels (see 2D settings page) is done using ledmaps (using customMappingTable)
* Custom Ledmaps therefore only possible in 1D not in 2D (changed in recent build: custom ledmaps overwrite panel setup)
* If ledmap files are uploaded you need to reboot in order for them to become effective !!!
* A ledmap can be applied in a preset or 'global' (global is in segments tab)
* A ledmap is specified in a dropdown which can have the following values: 
<img width="289" alt="image" src="https://user-images.githubusercontent.com/91013628/217567957-9cb55f75-dbe9-486f-abcd-39d1131a6fb5.png">

* Unchanged: nothing will happen (if a ledmap is active, that ledmap will stay active)
* Default: no ledmap applied (or if ledmap0.json is present that will be applied)
* Ledmap1.json to ledmap9.json. The ledmap to be applied

### 0.14 MM ☾
* Support of ledmaps in 2D using the customMappingTable both for physical mapping and for ledmapping (The map isn't in 2D coordinates, it's just linear remapping) 
* Ledmap properties:

<img width="222" alt="image" src="https://user-images.githubusercontent.com/91013628/223077405-2c37bec0-3d94-4ff8-9725-fdfca886f559.png">

   - n (name) and physical is not used yet
   - width and height define the total width and height of the 2D coordinate space (this overrides 2D configuration settings)

* Repository of ledmap examples: [WLED-Effects/Ledmaps](https://github.com/MoonModules/WLED-Effects/tree/master/Ledmaps) containing irregular 2D shapes (clouds and cube) and rings remapping (rings). For testing the different ledmaps upload presets.json in this folder to /edit
