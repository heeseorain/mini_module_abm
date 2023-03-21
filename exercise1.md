---
title: "Software exercise 1"
nav_order: 5
nav_exclude: false
search_exclude: true
---

<button class="btn js-toggle-dark-mode">Dark color scheme</button>

<script type="text/javascript" src="{{ "/assets/js/dark-mode-preview.js" | absolute_url }}"></script>

# Software exercise 1
### Teaching materials are prepared by Dr Heeseo Rain Kwon (heeseo.kwon.10@ucl.ac.uk). 

## Download and install NetLogo and QGIS
- Please download and install `NetLogo (6.2.1)` according to your platform (for Windows, download 64-bit): [NetLogo Download Page](https://ccl.northwestern.edu/netlogo/6.2.1/){:target="_blank"}.
- Please download and install `QGIS (3.28 LTR)` according to your platform: [QGIS Download Page](https://www.qgis.org/en/site/forusers/download.html#){:target="_blank"}.

## Instructions
1. Read through the instruction carefully. You may face problems if you overlook any of the steps.
2. Save your NetLogo and QGIS working files regularly.
3. When running tasks on NetLogo and QGIS, leave the settings as default unless instructed.

Note: functions and filename are `highlighted` in this document.

## Software exercise overview
In this exercise, you will get introduced to NetLogo through playing with "game of life" and "wolf sheep predation" models, preparing spatial input data on QGIS for an urban growth model, and how to use GIS extension to input raster maps on NetLogo.

## Introducing NetLogo (10min)

### Setup work environment for NetLogo
1. Launch NetLogo. The interface will be explained along with exercises. Note: You can refer to [NetLogo User Manual (6.2.1)](https://ccl.northwestern.edu/netlogo/6.2.1/docs/){:target="_blank"} for more information.
3. In `File` > `Models Library`, you can find a collection of sample models to explore. Note: You can find more on the [NetLogo User Community Models web page](http://ccl.northwestern.edu/netlogo/models/community/index.cgi) in your own time.

### Exercise 1: Wolf Sheep Predation
1. `Models Library` > `Biology` > `Wolf Sheep Predation`.

![](statics/Sup2_wolfsheep1.PNG)

2. Click `setup` > `go` to start the simulation, and click `go` again to stop the simulation.
3. Try running the model with following changes and explain what happens:
- Change the `model-version` to `sheep-wolves-grass`. Sheep and wolves are the moving agents (turtles in NetLogo), and grass form a grid of stationary agents (patches).
- Decrease wolf poplulation.
- What other sliders can you adjust to help out the sheep population?
- Can you find any parameters that generate a stable ecosystem?

![](statics/Sup2_wolfsheep2.PNG)
