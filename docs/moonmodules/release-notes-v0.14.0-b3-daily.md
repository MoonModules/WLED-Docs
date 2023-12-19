---
title: Release notes v0.14.0-b3-daily
hide:
  # - navigation
  # - toc
---

Below are the ongoing updates in WLEDMM which has not made it to a release yet (Next major release will be v0.14.0-b35)

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



