---
title: Mappings
hide:
  # - navigation
  # - toc
---

## Introduction

There are a few steps between an effect and it's physical presentation on a number of leds.

This are the basic steps:

* The effect creates for each segment frame a number of pixels using setPixelColor where pixel(0) is left (2D top left) and pixel(length) is right (2D: pixel(widthxheight), bottom right)
* Segments are mapped to a strip (2D: Matrix) again from left (top) to right (bottom). This is a logical mapping because the real wiring can be different (normally not in strips, but in matrix panels they are) - specify in segments tab
*  Logical strip (or matrix) is mapped to how they physically look. E.g. for matrix panels: where is the first pixel (top/bottom/left/right), how is the orientation (horizontal / vertical) and is it serpentine (or not). There can be multiple panels. - Specify in settings / 2D configuration

Optionally there can also be:

* JSON Mapping: Mapping of 1D effects to 2D. Expand1D (Logical mapping)
* Ledmaps: e.g. for custom setup using led strips, cubes or circles etc in a 2D layout. (Phyisical mapping)

Remarks

* All mappings use ledmap<x>.json style mappings. JSON Mapping supports 2D coordinates, the others not. Will be harmonized
* Peek should show Logical ledmaps, not physical ledmaps (except the now show pixels). 

## Mappings
Below is in processing order

### JSON mapping
AKA jmap
1D expansion: maps a 1D effect to a 2D pattern

From excel/vba <img width="181" alt="image" src="https://user-images.githubusercontent.com/1737159/188688306-b5a5e7d8-3172-43b8-9f53-778ff9a2df3b.png"> via /edit and <img width="98" alt="image" src="https://user-images.githubusercontent.com/1737159/188688993-34c73f35-b642-4120-b31d-c87ea58ea10e.png">
 to matrix <img width="160" alt="image" src="https://user-images.githubusercontent.com/1737159/188688601-73a9e7f8-34d9-463f-9ec3-1cacaea13d6b.png">

Files are here: [JSONMappings](https://github.com/MoonModules/WLED-Effects/tree/master/JSONMappings)

json files need to be uploaded to /edit. E.g. if filename is candle33.json, the name of the segment must be candle33 and expand1D must be jmap in order to run the mapping.
  
### Segment to Logical
Maps segments to a matrix where (0,0) is always topleft and (width, height) always bottom right.
Non serpentine

### Panel layout
Takes into account Panel setup and Led panel layout as defined in 2D Configuration (e.g. 1st panel, 1st led, serpentine)

Code: uses customMappingTable

### Ledmaps
* Shuffles leds
* Both for 1 and 2D
* Ledmaps override panel layout !!

Code: uses customMappingTable

See also [Advanced/Mappings](/advanced/mapping/)

## Fork specific info

| Feature | [WLED SR 0.13](https://github.com/atuline/WLED/tree/dev) | [MoonModules WLED 0.14](https://github.com/MoonModules/WLED/tree/mdev) | [Upstream WLED 0.14](https://github.com/Aircoookie/WLED) |
|---|---|---|---|
JSON Mapping|No|Yes|No JSON mapping yet although it's based on an idea from AirCoookie 
Segment to Logical|Yes|Yes|Yes
Ledmaps|Yes|Yes|Yes
Panel layout|Yes|Yes|Yes

