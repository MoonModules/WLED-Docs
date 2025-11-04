---
title: 2D and 1D Mixed Setup
hide:
  # - navigation
  # - toc
---

## Overview
🌜

WLED-MM supports mixing 2D and 1D setup on the same unit, the expected result is that you could use 2D fixture and still chain a strip after or setup a strip and then a matrix after on the same pin.

!!! important 
    The necessary steps are different from upstream WLED. In WLED-MM, you create a "pseudo" 2D panel for the trailing strip, then set "Expand 1D FX" to "Pixels" in segment options.
    
> As WLED-SR has introduced 2D panels long before upstream WLED, we are still using the original approach for mixed setups. As a benefit, you will be able to create interesting effects by running a 2D effects "flat" on a pseudo 2D panel (example: GEQ 2D on a pseudo 16x6 panel -> puts all bars next to each other on the strip)


1. Setup your total LED count in Config -> LED Preferences as usual. For example a 8x8 matrix and a strip of 30 pixels chained to the end of your matrix. The total count should be 64 + 30 = 94. This also works with virtual LEDs via DDP or ArtNet.
2. Go to Config -> 2D setup and create the 8x8 matrix, and a second matrix panel for the trailing strip.
3. For larger pixel counts, you should chose square dimensions like 5x6. For smaller pixel counts, create a panel with only one row, like 30x1.
4. Position the "pseudo" 2D panel at the right / top side of your "real" 8x8 matrix panel => offset X = 8, offset Y = 0. Another possibility is to place the "pseudo" panel below your normal panel in 2D settings.
5. Now create segments for both 2D panels. click on the segment for your trailing strip, select a 1D effect, then change "Expand 1D FX" to "Pixels" in segment options.
6. You might need to experiment with "Reverse X" , "Reverse Y", and "Transpose" options, to make the effect behave correctly.
7. Save your segment, create a new preset for the current setup. Its recommended to set this preset as startup preset in LEDs settings.


Note: some "pseudo" 2D layouts are automaticially detected by WLED-MM. For these cases, 1D effects will run as expected, but you might not see the  "Expand 1D FX" segment option.

!!! Tip
    A user has posted a [set of screenshots here](https://github.com/MoonModules/WLED-MM/issues/79#issuecomment-2068537606) that guide through all steps.
