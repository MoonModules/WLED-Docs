---
title: Segment Masks
hide:
  # - navigation
  # - toc
---

## Introduction

Segment masks add per-segment clipping. A mask defines which virtual pixels a segment is allowed to draw. Pixels outside the mask are left untouched, which makes foreground and background layering easy with overlapping segments.

Segment masks do not remap LEDs. They clip after the segment's normal mapping (start/stop, 2D layout, panel layout, ledmap, etc.).

## Mask files (segmaskX.json)

Mask files live on the filesystem and follow the same upload flow as ledmaps:

- Upload via `/edit`
- File name pattern: `segmask1.json`, `segmask2.json`, ...
- `segmask0.json` is reserved (0 means no mask)

### Format

```json
{"w":4,"h":4,"inv":false,"mask":[0,0,1,0,0,1,1,0,0,1,1,0,0,0,1,0]}
```

Fields:

- `w` and `h` define the mask dimensions in virtual pixels.
- `mask` is a flat array of `0` or `1` values, length must equal `w*h`.
- `inv` is optional and inverts the mask (true or false only).

Notes:

- Index order is row-major: `index = x + (y * w)` with `(0,0)` at the top-left.
- Parsing is strict: only `0` and `1` are accepted in `mask`, and `inv` accepts only `true` or `false`.
- If `w` and `h` do not match the segment's virtual size, the mask is ignored.

## Using masks in 1D setups

1. Create a file like `segmask1.json` with `w = segment length` and `h = 1`.
2. Upload it via `/edit`.
3. Reboot WLED to load the new mask files.
4. In the segment UI, pick the mask file in the Mask dropdown.
5. (Optional) enable Invert mask to draw outside the shape instead of inside.

Tip: Use two overlapping segments for a clean foreground/background effect.

- Segment 0: full length, background effect/palette
- Segment 1: same bounds, mask enabled, foreground effect/palette

## Using masks in 2D setups

1. Choose a segment that spans the desired matrix area.
2. Ensure the mask dimensions match the segment's virtual size.
   - Example: a 32x16 matrix mask needs `w = 32`, `h = 16`.
3. Upload `segmaskX.json` via `/edit`.
4. Reboot WLED to load the new mask files.
5. Pick the mask file in the segment Mask dropdown.

You can still use Expand 1D FX for 1D effects on 2D segments; the mask clips the final output.

## UI notes

- Mask selection does not disable segment bounds or geometry options; they still apply to the masked output.

## Interaction with other mappings

- Ledmaps and panel layout still define physical wiring order.
- Masks only clip what the segment draws; they do not change LED order.
- JSON Mapping (jmap) is still applied before the mask.

## Memory and performance

Masks use 1 bit per pixel in the segment's virtual space. Example: a 32x32 mask uses 1024 bits (128 bytes). Clipping is performed with bitwise operations for efficiency. Performance impact will be highest when layering complex effects, many segments, or large masks.

## JSON API usage

Segment state includes:

- `"mask"`: mask id (0 disables)
- `"minv"`: invert mask (true or false)

Example:

```json
{"seg":[{"id":0,"start":0,"stop":512},{"id":1,"start":0,"stop":512,"mask":1,"minv":false}]}
```
