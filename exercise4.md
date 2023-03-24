---
title: "Software exercise 4"
nav_order: 5
nav_exclude: false
search_exclude: true
---

<button class="btn js-toggle-dark-mode">Dark color scheme</button>

<script type="text/javascript" src="{{ "/assets/js/dark-mode-preview.js" | absolute_url }}"></script>

# Software exercise 4: Using QGIS and Excel with NetLogo (20 minutes)
### Teaching materials are prepared by Dr Heeseo Rain Kwon (heeseo.kwon.10@ucl.ac.uk). 

### Example 1: Linking census data with turtles using CSV extension (10min)
- Go through at your own pace.
- To show you how CSV extension works, we will continue to use the Isobenefit model from the previous exercise.

1. If not already opened, open the file `22mar2023_isobenefit_new_forest_hrkwon.nlogo`.

2. Download the census microdata of the case area: [census_2011_new_forest.csv](https://github.com/heeseorain/mini_module_abm/blob/master/data/census_2011_new_forest.csv){:target="_blank"} and save it in your working directory (e.g. your "mini_module_abm" folder).
- Note: I've prepared this csv file for this exercise session based on the 2011 Census microdata. For more information, see [Census 2021 microdata](https://www.ons.gov.uk/census/2011census/2011censusdata/censusmicrodata){:target="_blank"}. If you want, you can download the Microdata Teaching File and explore in your own time.

3. Open the file and have a quick look.

   ![](statics/census1.png)

4. In the `Code` tab of the `22mar2023_isobenefit_new_forest_hrkwon.nlogo` model, insert the following at the very bottom.

```
to read_2011_residents_from_csv
  file-close-all ; close all open files
  file-open "data/3624_turtles_2011_new_forest.csv" ; open the file with the turtle data

  ; We'll read all the data in a single loop
  while [ not file-at-end? ] [
    ; here the CSV extension grabs a single line and puts the read data in a list
    let data csv:from-row file-read-line
    ; now we can use that list to create a turtle with the saved properties
    create-turtles 1 [
      set xcor     random-xcor
      set ycor     random-ycor
      set size     3
      set shape    "circle"
      set caseno_2011           item 0 data  ;; 0=column A in excel. 1=column B. ... 29=colum AE.
      set prev_address_2011     item 1 data
      set age_2011              item 2 data
      set distance_to_work_2011 item 3 data
      set no_of_cars_2011       item 4 data
      set country_birth_2011    item 5 data
      set deprived_edu_2011     item 6 data
      set deprived_employ_2011  item 7 data
      set deprived_health_2011  item 8 data
      set deprived_housing_2011  item 9 data
      set deprived_2011         item 10 data
      set health_activity_limited_2011 item 11 data
      set child_2011            item 12 data
      set ethnicity_2011        item 13 data
      set general_health_2011   item 14 data
      set edu_2011              item 15 data
      set illness_in_house_2011 item 16 data
      set occupation_2011       item 17 data
      set prev_region_2011      item 18 data
      set social_grade_2011     item 19 data
      set sex_2011              item 20 data
      set tenure_2011           item 21 data
      set travel_mode_to_work_2011 item 22 data
      set travel_mode_to_work_2001 item 23 data
      set place_of_work_2011 item 24 data
      set live_near_work_2011 item 25 data
      set workplace_2011 item 26 data
    ]
  ]
end
```

