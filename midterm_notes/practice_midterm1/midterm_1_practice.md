---
title: "Midterm 1"
author: "Lejla Becirevic"
date: "2024-02-06"
output:
  html_document: 
    theme: spacelab
    keep_md: true
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your code should be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run. Be sure to add your name to the author header above. You may use any resources to answer these questions, but you may not post questions to Open Stacks or external help sites. There are 15 total questions, each is worth 2 points.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the tidyverse
If you plan to use any other libraries to complete this assignment then you should load them here.

```r
library(tidyverse)
```

```
## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
## ✔ dplyr     1.1.4     ✔ readr     2.1.5
## ✔ forcats   1.0.0     ✔ stringr   1.5.1
## ✔ ggplot2   3.4.4     ✔ tibble    3.2.1
## ✔ lubridate 1.9.3     ✔ tidyr     1.3.1
## ✔ purrr     1.0.2     
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```

```r
library(janitor)
```

```
## 
## Attaching package: 'janitor'
## 
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```


```r
getwd()
```

```
## [1] "/Users/lejla.becirevic/Desktop/BIS15W2024_lbecirevic/midterm_notes/practice_midterm1"
```

## Questions  

Wikipedia's definition of [data science](https://en.wikipedia.org/wiki/Data_science): "Data science is an interdisciplinary field that uses scientific methods, processes, algorithms and systems to extract knowledge and insights from noisy, structured and unstructured data, and apply knowledge and actionable insights from data across a broad range of application domains."  

1. (2 points) Consider the definition of data science above. Although we are only part-way through the quarter, what specific elements of data science do you feel we have practiced? Provide at least one specific example.  

2. (2 points) What is the most helpful or interesting thing you have learned so far in BIS 15L? What is something that you think needs more work or practice?  

In the midterm 1 folder there is a second folder called `data`. Inside the `data` folder, there is a .csv file called `ElephantsMF`. These data are from Phyllis Lee, Stirling University, and are related to Lee, P., et al. (2013), "Enduring consequences of early experiences: 40-year effects on survival and success among African elephants (Loxodonta africana)," Biology Letters, 9: 20130011. [kaggle](https://www.kaggle.com/mostafaelseidy/elephantsmf).  

3. (2 points) Please load these data as a new object called `elephants`. Use the function(s) of your choice to get an idea of the structure of the data. Be sure to show the class of each variable.

```r
elephants <- read_csv("data/ElephantsMF.csv")
```

```
## Rows: 288 Columns: 3
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (1): Sex
## dbl (2): Age, Height
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

4. (2 points) Change the names of the variables to lower case and change the class of the variable `sex` to a factor.

```r
elephants <- clean_names(elephants)
```


```r
elephants$sex <- as.factor(elephants$sex)
```


5. (2 points) How many male and female elephants are represented in the data?

```r
elephants %>% 
  filter(sex=="M") %>% 
  summarize(males=n())
```

```
## # A tibble: 1 × 1
##   males
##   <int>
## 1   138
```


```r
elephants %>% 
  filter(sex=="F") %>% 
  summarize(females=n())
```

```
## # A tibble: 1 × 1
##   females
##     <int>
## 1     150
```


```r
elephants %>% 
  group_by(sex) %>% 
  summarize(total=n())
```

```
## # A tibble: 2 × 2
##   sex   total
##   <fct> <int>
## 1 F       150
## 2 M       138
```


```r
elephants %>% 
  count(sex)
```

```
## # A tibble: 2 × 2
##   sex       n
##   <fct> <int>
## 1 F       150
## 2 M       138
```

6. (2 points) What is the average age all elephants in the data?

```r
elephants %>% 
  summarize(mean_age=mean(age))
```

```
## # A tibble: 1 × 1
##   mean_age
##      <dbl>
## 1     11.0
```


7. (2 points) How does the average age and height of elephants compare by sex?

```r
elephants %>% 
  filter(sex=="F") %>% 
  summarize(mean_age_f=mean(age),
            mean_height_f=mean(height))
```

```
## # A tibble: 1 × 2
##   mean_age_f mean_height_f
##        <dbl>         <dbl>
## 1       12.8          190.
```


```r
elephants %>% 
  filter(sex=="M") %>% 
  summarize(mean_age_m=mean(age),
            mean_height_m=mean(height))
```

```
## # A tibble: 1 × 2
##   mean_age_m mean_height_m
##        <dbl>         <dbl>
## 1       8.95          185.
```


```r
elephants %>% 
  group_by(sex) %>% 
  summarize(mean_age=mean(age),
            mean_height=mean(height))
```

```
## # A tibble: 2 × 3
##   sex   mean_age mean_height
##   <fct>    <dbl>       <dbl>
## 1 F        12.8         190.
## 2 M         8.95        185.
```


8. (2 points) How does the average height of elephants compare by sex for individuals over 20 years old. Include the min and max height as well as the number of individuals in the sample as part of your analysis.  

```r
elephants %>% 
  filter(age>=20) %>% 
  filter(sex=="M") %>% 
  summarize(mean_height_m=mean(height),
            min_height_m=min(height),
            max_height_m=max(height),
            total=n())
```

```
## # A tibble: 1 × 4
##   mean_height_m min_height_m max_height_m total
##           <dbl>        <dbl>        <dbl> <int>
## 1          270.         229.         304.    13
```


```r
elephants %>% 
  filter(age>=20) %>% 
  filter(sex=="F") %>% 
  summarize(mean_height_f=mean(height),
            min_height_f=min(height),
            max_height_f=max(height),
            total=n())
```

```
## # A tibble: 1 × 4
##   mean_height_f min_height_f max_height_f total
##           <dbl>        <dbl>        <dbl> <int>
## 1          232.         193.         278.    37
```


```r
elephants %>% 
  filter(age>20) %>% 
  group_by(sex) %>% 
  summarize(mean_height=mean(height),
            min_height=min(height),
            max_height=max(height),
            total_individuals=n())
```

```
## # A tibble: 2 × 5
##   sex   mean_height min_height max_height total_individuals
##   <fct>       <dbl>      <dbl>      <dbl>             <int>
## 1 F            232.       193.       278.                37
## 2 M            270.       229.       304.                13
```

For the next series of questions, we will use data from a study on vertebrate community composition and impacts from defaunation in [Gabon, Africa](https://en.wikipedia.org/wiki/Gabon). One thing to notice is that the data include 24 separate transects. Each transect represents a path through different forest management areas.  

Reference: Koerner SE, Poulsen JR, Blanchard EJ, Okouyi J, Clark CJ. Vertebrate community composition and diversity declines along a defaunation gradient radiating from rural villages in Gabon. _Journal of Applied Ecology_. 2016. This paper, along with a description of the variables is included inside the midterm 1 folder.  

9. (2 points) Load `IvindoData_DryadVersion.csv` and use the function(s) of your choice to get an idea of the overall structure. Change the variables `HuntCat` and `LandUse` to factors.

```r
vertebrate <- read_csv("data/IvindoData_DryadVersion.csv")
```

```
## Rows: 24 Columns: 26
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (2): HuntCat, LandUse
## dbl (24): TransectID, Distance, NumHouseholds, Veg_Rich, Veg_Stems, Veg_lian...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


```r
vertebrate <- clean_names(vertebrate)
```


```r
names(vertebrate)
```

```
##  [1] "transect_id"              "distance"                
##  [3] "hunt_cat"                 "num_households"          
##  [5] "land_use"                 "veg_rich"                
##  [7] "veg_stems"                "veg_liana"               
##  [9] "veg_dbh"                  "veg_canopy"              
## [11] "veg_understory"           "ra_apes"                 
## [13] "ra_birds"                 "ra_elephant"             
## [15] "ra_monkeys"               "ra_rodent"               
## [17] "ra_ungulate"              "rich_all_species"        
## [19] "evenness_all_species"     "diversity_all_species"   
## [21] "rich_bird_species"        "evenness_bird_species"   
## [23] "diversity_bird_species"   "rich_mammal_species"     
## [25] "evenness_mammal_species"  "diversity_mammal_species"
```


```r
summary(vertebrate)
```

```
##   transect_id       distance        hunt_cat         num_households 
##  Min.   : 1.00   Min.   : 2.700   Length:24          Min.   :13.00  
##  1st Qu.: 5.75   1st Qu.: 5.668   Class :character   1st Qu.:24.75  
##  Median :14.50   Median : 9.720   Mode  :character   Median :29.00  
##  Mean   :13.50   Mean   :11.879                      Mean   :37.88  
##  3rd Qu.:20.25   3rd Qu.:17.683                      3rd Qu.:54.00  
##  Max.   :27.00   Max.   :26.760                      Max.   :73.00  
##    land_use            veg_rich       veg_stems       veg_liana     
##  Length:24          Min.   :10.88   Min.   :23.44   Min.   : 4.750  
##  Class :character   1st Qu.:13.10   1st Qu.:28.69   1st Qu.: 9.033  
##  Mode  :character   Median :14.94   Median :32.45   Median :11.940  
##                     Mean   :14.83   Mean   :32.80   Mean   :11.040  
##                     3rd Qu.:16.54   3rd Qu.:37.08   3rd Qu.:13.250  
##                     Max.   :18.75   Max.   :47.56   Max.   :16.380  
##     veg_dbh        veg_canopy    veg_understory     ra_apes      
##  Min.   :28.45   Min.   :2.500   Min.   :2.380   Min.   : 0.000  
##  1st Qu.:40.65   1st Qu.:3.250   1st Qu.:2.875   1st Qu.: 0.000  
##  Median :43.90   Median :3.430   Median :3.000   Median : 0.485  
##  Mean   :46.09   Mean   :3.469   Mean   :3.020   Mean   : 2.045  
##  3rd Qu.:50.58   3rd Qu.:3.750   3rd Qu.:3.167   3rd Qu.: 3.815  
##  Max.   :76.48   Max.   :4.000   Max.   :3.880   Max.   :12.930  
##     ra_birds      ra_elephant       ra_monkeys      ra_rodent    
##  Min.   :31.56   Min.   :0.0000   Min.   : 5.84   Min.   :1.060  
##  1st Qu.:52.51   1st Qu.:0.0000   1st Qu.:22.70   1st Qu.:2.047  
##  Median :57.90   Median :0.3600   Median :31.74   Median :3.230  
##  Mean   :58.64   Mean   :0.5450   Mean   :31.30   Mean   :3.278  
##  3rd Qu.:68.17   3rd Qu.:0.8925   3rd Qu.:39.88   3rd Qu.:4.093  
##  Max.   :85.03   Max.   :2.3000   Max.   :54.12   Max.   :6.310  
##   ra_ungulate     rich_all_species evenness_all_species diversity_all_species
##  Min.   : 0.000   Min.   :15.00    Min.   :0.6680       Min.   :1.966        
##  1st Qu.: 1.232   1st Qu.:19.00    1st Qu.:0.7542       1st Qu.:2.248        
##  Median : 2.545   Median :20.00    Median :0.7760       Median :2.317        
##  Mean   : 4.166   Mean   :20.21    Mean   :0.7699       Mean   :2.310        
##  3rd Qu.: 5.157   3rd Qu.:22.00    3rd Qu.:0.8083       3rd Qu.:2.429        
##  Max.   :13.860   Max.   :24.00    Max.   :0.8330       Max.   :2.566        
##  rich_bird_species evenness_bird_species diversity_bird_species
##  Min.   : 8.00     Min.   :0.5590        Min.   :1.162         
##  1st Qu.:10.00     1st Qu.:0.6825        1st Qu.:1.603         
##  Median :11.00     Median :0.7220        Median :1.680         
##  Mean   :10.33     Mean   :0.7137        Mean   :1.661         
##  3rd Qu.:11.00     3rd Qu.:0.7722        3rd Qu.:1.784         
##  Max.   :13.00     Max.   :0.8240        Max.   :2.008         
##  rich_mammal_species evenness_mammal_species diversity_mammal_species
##  Min.   : 6.000      Min.   :0.6190          Min.   :1.378           
##  1st Qu.: 9.000      1st Qu.:0.7073          1st Qu.:1.567           
##  Median :10.000      Median :0.7390          Median :1.699           
##  Mean   : 9.875      Mean   :0.7477          Mean   :1.698           
##  3rd Qu.:11.000      3rd Qu.:0.7847          3rd Qu.:1.815           
##  Max.   :12.000      Max.   :0.8610          Max.   :2.065
```


```r
glimpse(vertebrate)
```

```
## Rows: 24
## Columns: 26
## $ transect_id              <dbl> 1, 2, 2, 3, 4, 5, 6, 7, 8, 9, 13, 14, 15, 16,…
## $ distance                 <dbl> 7.14, 17.31, 18.32, 20.85, 15.95, 17.47, 24.0…
## $ hunt_cat                 <chr> "Moderate", "None", "None", "None", "None", "…
## $ num_households           <dbl> 54, 54, 29, 29, 29, 29, 29, 54, 25, 73, 46, 5…
## $ land_use                 <chr> "Park", "Park", "Park", "Logging", "Park", "P…
## $ veg_rich                 <dbl> 16.67, 15.75, 16.88, 12.44, 17.13, 16.50, 14.…
## $ veg_stems                <dbl> 31.20, 37.44, 32.33, 29.39, 36.00, 29.22, 31.…
## $ veg_liana                <dbl> 5.78, 13.25, 4.75, 9.78, 13.25, 12.88, 8.38, …
## $ veg_dbh                  <dbl> 49.57, 34.59, 42.82, 36.62, 41.52, 44.07, 51.…
## $ veg_canopy               <dbl> 3.78, 3.75, 3.43, 3.75, 3.88, 2.50, 4.00, 4.0…
## $ veg_understory           <dbl> 2.89, 3.88, 3.00, 2.75, 3.25, 3.00, 2.38, 2.7…
## $ ra_apes                  <dbl> 1.87, 0.00, 4.49, 12.93, 0.00, 2.48, 3.78, 6.…
## $ ra_birds                 <dbl> 52.66, 52.17, 37.44, 59.29, 52.62, 38.64, 42.…
## $ ra_elephant              <dbl> 0.00, 0.86, 1.33, 0.56, 1.00, 0.00, 1.11, 0.4…
## $ ra_monkeys               <dbl> 38.59, 28.53, 41.82, 19.85, 41.34, 43.29, 46.…
## $ ra_rodent                <dbl> 4.22, 6.04, 1.06, 3.66, 2.52, 1.83, 3.10, 1.2…
## $ ra_ungulate              <dbl> 2.66, 12.41, 13.86, 3.71, 2.53, 13.75, 3.10, …
## $ rich_all_species         <dbl> 22, 20, 22, 19, 20, 22, 23, 19, 19, 19, 21, 2…
## $ evenness_all_species     <dbl> 0.793, 0.773, 0.740, 0.681, 0.811, 0.786, 0.8…
## $ diversity_all_species    <dbl> 2.452, 2.314, 2.288, 2.006, 2.431, 2.429, 2.5…
## $ rich_bird_species        <dbl> 11, 10, 11, 8, 8, 10, 11, 11, 11, 9, 11, 11, …
## $ evenness_bird_species    <dbl> 0.732, 0.704, 0.688, 0.559, 0.799, 0.771, 0.8…
## $ diversity_bird_species   <dbl> 1.756, 1.620, 1.649, 1.162, 1.660, 1.775, 1.9…
## $ rich_mammal_species      <dbl> 11, 10, 11, 11, 12, 12, 12, 8, 8, 10, 10, 11,…
## $ evenness_mammal_species  <dbl> 0.736, 0.705, 0.650, 0.619, 0.736, 0.694, 0.7…
## $ diversity_mammal_species <dbl> 1.764, 1.624, 1.558, 1.484, 1.829, 1.725, 1.9…
```


```r
vertebrate$hunt_cat <- as.factor(vertebrate$hunt_cat)
vertebrate$land_use <- as.factor(vertebrate$land_use)
```

10. (4 points) For the transects with high and moderate hunting intensity, how does the average diversity of birds and mammals compare?


```r
vertebrate %>% 
  group_by(hunt_cat) %>% 
  summarise(mean_bird_diversity=mean(diversity_bird_species),
            mean_mammal_diversity=mean(diversity_mammal_species),
            total=n())
```

```
## # A tibble: 3 × 4
##   hunt_cat mean_bird_diversity mean_mammal_diversity total
##   <fct>                  <dbl>                 <dbl> <int>
## 1 High                    1.66                  1.74     7
## 2 Moderate                1.62                  1.68     8
## 3 None                    1.70                  1.68     9
```


11. (4 points) One of the conclusions in the study is that the relative abundance of animals drops off the closer you get to a village. Let's try to reconstruct this (without the statistics). How does the relative abundance (RA) of apes, birds, elephants, monkeys, rodents, and ungulates compare between sites that are less than 3km from a village to sites that are greater than 25km from a village? The variable `Distance` measures the distance of the transect from the nearest village. Hint: try using the `across` operator.  

```r
vertebrate %>% 
  filter(distance<3) %>% 
  summarise(across(contains("RA_"), mean))
```

```
## # A tibble: 1 × 6
##   ra_apes ra_birds ra_elephant ra_monkeys ra_rodent ra_ungulate
##     <dbl>    <dbl>       <dbl>      <dbl>     <dbl>       <dbl>
## 1    0.12     76.6       0.145       17.3      3.90        1.87
```


```r
vertebrate %>% 
  filter(distance>25) %>% 
  summarise(across(contains("RA_"), mean))
```

```
## # A tibble: 1 × 6
##   ra_apes ra_birds ra_elephant ra_monkeys ra_rodent ra_ungulate
##     <dbl>    <dbl>       <dbl>      <dbl>     <dbl>       <dbl>
## 1    4.91     31.6           0       54.1      1.29        8.12
```

12. (4 points) Based on your interest, do one exploratory analysis on the `gabon` data of your choice. This analysis needs to include a minimum of two functions in `dplyr.`

```r
vertebrate %>% 
  select(ra_birds, ra_elephant) %>% 
  filter(ra_birds>=60) %>% 
  filter(ra_elephant>=0.5)
```

```
## # A tibble: 4 × 2
##   ra_birds ra_elephant
##      <dbl>       <dbl>
## 1     73.1        2.2 
## 2     74.4        0.99
## 3     66.6        0.52
## 4     68.2        0.77
```

