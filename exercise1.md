---
title: "Software exercise 1"
nav_order: 5
nav_exclude: false
search_exclude: true
---

<button class="btn js-toggle-dark-mode">Dark color scheme</button>

<script type="text/javascript" src="{{ "/assets/js/dark-mode-preview.js" | absolute_url }}"></script>

# Software exercise 1 (60 minutes)
### Teaching materials are prepared by Dr Heeseo Rain Kwon (heeseo.kwon.10@ucl.ac.uk). 

## Download and install NetLogo and QGIS
- Please download and install `NetLogo (6.2.1)` according to your platform (for Windows, download 64-bit): [NetLogo Download Page](https://ccl.northwestern.edu/netlogo/6.2.1/){:target="_blank"}.
- Please download and install `QGIS (3.28 LTR)` according to your platform: [QGIS Download Page](https://www.qgis.org/en/site/forusers/download.html#){:target="_blank"}. If you already have QGIS in your laptop and if you have used QGIS before, feel free to use your version while some options etc. might be slightly different.

## Instructions
1. Read through the instruction carefully. You may face problems if you overlook any of the steps.
2. If you wish to save your changes, save your NetLogo and QGIS file regularly.
3. When running tasks on NetLogo and QGIS, leave the settings as default unless instructed.

Note: functions and filename are `highlighted` in this document.

## Software exercise overview
In this exercise, you will get introduced to NetLogo through playing with "game of life" and "wolf sheep predation" models, preparing spatial input data on QGIS for an urban growth model, and how to use GIS extension to input raster maps on NetLogo.

## Introducing NetLogo (30min)

### Setup work environment for NetLogo
1. Open `NetLogo 6.2.1` (NOT `NetLogo 3D 6.2.1`). The interface will be explained along with exercises. Note: You can refer to [NetLogo User Manual (6.2.1)](https://ccl.northwestern.edu/netlogo/6.2.1/docs/){:target="_blank"} for more information.
3. In `File` > `Models Library`, you can find a collection of sample models to explore. Note: You can find more on the [NetLogo User Community Models web page](http://ccl.northwestern.edu/netlogo/models/community/index.cgi){:target="_blank"} in your own time.

### Exercise 1: Game of Life and understanding NetLogo codes (10min)
- Go through at your own pace.

1. `File` > `Models Library` > `Computer Science` > `Cellular Automata` > `Life`.
- Game of Life is a simple cellular automata (CA) model where the state of the cells (patches) change according to behavioral rules. 
- As the simulation runs, you can find recurring shapes like gliders and blinkers. 
- Note: You can quickly scroll through [Conway's Game of Life](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life){:target="_blank"} to get a quick idea. Another good read in your own time is [The Lasting Lessons of John Conway's Game of Life](https://www.nytimes.com/2020/12/28/science/math-conway-game-of-life.html){:target="_blank"}.

![](statics/life1.png)

2. Click `setup-random` > `go-forever` to start the simulation, and click `go-forever` again to stop the simulation.

3. Let's check the `Code` tab. 
- Note: If you don't see line numbers, for Windows users, on the `Menu bar`, click `Tools` > `Preferences` and check `Show Line Numbers`. 
- For Mac users, on the `Menu bar`, click `NetLogo` > `Preferences` and check `Show Line Numbers`. 

5. In line 2-3, `living?` and `live-neighbors` are variables. 
- In line 8, `ask patches [ cell-death ]` means to [ask](http://ccl.northwestern.edu/netlogo/docs/dict/ask.html){:target="_blank"} patches to run the `[ cell-death ]` command. 
- In line 26, `[ cell-death ]` command sets `living?` as false, and sets patch color as foreground color. `[ cell-birth ]` command does the opposite.

6. Line 14 means "ask patches to run the [ifelse](http://ccl.northwestern.edu/netlogo/docs/dict/ifelse.html){:target="_blank"} command. ifelse commands are very important in language-based rules. 
- Line 15-17 means "if `random-float 100 < initial-density` reports true (in other words, "if a `random floating point number >= 0 but less than 100` is less than the `initial density (default=35)`"), run the `[ cell-birth ]` command, and otherwise, run the `[ cell-death ]` command. 
- This part makes each cell to check the state of itself.
- Note: You can refer to [NetLogo Dictionary](http://ccl.northwestern.edu/netlogo/docs/index2.html){:target="_blank"} when trying to understand the codes.

![](statics/Sup2_gameoflife2.PNG)

7. Line 33 means "set the variable `live-neighbors` to `count how many neighboring cells are alive`" and line 32 asks patches to run this command. 
- This part makes each cell to check the state of its eight surrounding neighbors. Note: Refer to [neighbors](http://ccl.northwestern.edu/netlogo/docs/dict/neighbors.html){:target="_blank"}.

8. Line 38 asks patches to run another ifelse command. 

### Exercise 1: Questions (10min):
- Please write all your answers in a notepad (paper or laptop). We will go through the answers together.
- Go through at your own pace. If you don't manage to go through all Qs, you can resume in the final session (5pm). If you finish quickly, feel free to start [[Exercise 4]](./exercise4.md){:target="_blank"}.

Q1. Click the `Info` tab below the `Menu bar`. Under `HOW IT WORKS`, you can find the rules of the game. Rules can be summarised as the four points below. 
1. If there is exactly 3 alive neighbors, the cell becomes alive. (birth)
2. If there are less than 2 alive neighbors, the cell dies. (under-population)
3. If there are more than 3 alive neighbors, the cell dies. (over-population)
4. If there are 2 alive neighbors, the cell remains in the state it is in. (sustainable life)

Q1-1. Try writing these rules into NetLogo code using [if](http://ccl.northwestern.edu/netlogo/docs/dict/if.html){:target="_blank"} statement, one line of code for the first three points (Note: You don't need to worry about the 4th point because it doesn't change the cell state). 

Q1.2. Explain how these three lines of code can be shorted to line 39-42 written in the model using the [ifelse](http://ccl.northwestern.edu/netlogo/docs/dict/ifelse.html){:target="_blank"}.

![](statics/Sup2_gameoflife3.PNG)

Q2. In line 33, try changing `neighbors` to `neighbors4` and run the model. Observe and explain how this change affects the simulation. (Refer to [neighbors4](http://ccl.northwestern.edu/netlogo/docs/dict/neighbors.html).)

Q3. Let's add one additional command to the model. Add the following lines below the `to cell-death` part. This command makes this cell colored in green to kill the four surrounding patches.  Explain this rule in your own words. 
- Note: In case you don't see green zombie cells appearing, you change the `neighbors4` back to `neighbors` as in the screenshot below and set the initial-density around 35% so that cells don't die out too quickly. Also, try pressing "go-once" several times rather than "go-forever".
```
to zombie-birth
  set living? true
  ask neighbors [ cell-death ]
  set pcolor green
end
```
![](statics/Sup2_gameoflife4.PNG)

Q4. Let's add a new rule for `zombie-birth`. Add the following lines below the `ask patches [ ifelse ]` part. This rule runs the same ifelse command on the 1,000 randomly chosen patches, this time for `zombie-birth`.
- Note: [n-of](http://ccl.northwestern.edu/netlogo/docs/dict/n-of.html). Run the model and explain how this change affects the simulation.
```
ask n-of 1000 patches
  [ ifelse live-neighbors = 3
    [ zombie-birth ]
    [if live-neighbors != 2
      [ cell-death ] ] ]
```         
![](statics/Sup2_gameoflife5.PNG)


### Exercise 2: Wolf Sheep Predation and understanding parameters, turtles and patches (5min)
1. `File` > `Models Library` > `Biology` > `Wolf Sheep Predation`.

![](statics/Sup2_wolfsheep1.PNG)
![](statics/Sup2_wolfsheep2.PNG)

### Exercise 2: Questions (10min): 
- We will go through these together.

Q1. Click `setup` > `go` to start the simulation, and click `go` again to stop the simulation.
- With these initial parameter settings, what happens?
- Try running the model a few times. Do you get the same results or different? Why do you think so?

Q2. Try running the model with following changes:
- Decrease `initial-number-wolves` to 20. What happens? How does the plot help you explain what happened?
- Set `initial-number-sheep` to 80 and `initial-number-wolf` to 50. Set `sheep-reproduce` to 10.0%. Run the simulation. What happens?

Q3. Currently, one more important agent of the ecosystem is missing - grass.
- Change the `model-version` to `sheep-wolves-grass`. Sheep and wolves are the moving agents (turtles in NetLogo), and grass form a grid of stationary agents (patches).
- How does including grass in the model affect the sheep and wolf population?

## Introducing QGIS and using it with NetLogo (30min)

### QGIS project setup
1. Create a folder at your preferred directory on your disk (e.g. "abm" in Desktop). This folder will be the working directory for all the files.
2. Open QGIS 3.28.4.
3. Click `Project` > `New`.
4. Click `Project` > `Save As`, and save as `newforest.qgz` to the working directory. 

### Exercise 3: Preparing spatial input data on QGIS for an urban growth model
- As an example of an urban growth model, we will use [Isobenefit Urbanism morphogenesis](https://www.sciencedirect.com/science/article/pii/S0301479719307571) currently being reimplemented by H.R.Kwon (2023) as part of a project led by Dr Tommaso Gabrieli at UCL. 
- We will use data of a small part of [New Forest District](https://www.google.com/maps/place/New+Forest+District/) which includes Milford on Sea and Lymington.

1. Download boundary map of the case area: [ward_milford_lymington.zip](https://github.com/heeseorain/mini_module_abm/blob/master/data/ward_milford_lymington.zip){:target="_blank"} and save 
- Note: This boundary map is extracted from the [Ordinance Survey Data Hub](https://osdatahub.os.uk/downloads/open/BoundaryLine). If you're interested in accessing spatial data for different parts of UK, OS Data Hub is a good source.
2. Download land use map of the case area: [ukland_4841866_milford_lymington.zip](https://github.com/heeseorain/mini_module_abm/blob/master/data/ukland_4841866_milford_lymington.zip){:target="_blank"}.
- Note: This land use map is extracted from the "UKLand" data of [Verisk Data Download](https://digimap.edina.ac.uk/roam/download/verisk){:target="_blank"}. [Edina Digimap](https://digimap.edina.ac.uk/) is a great source for spatial data - if you're interested, log in with your UCL account and try exploring what's available. 

3. Load 

