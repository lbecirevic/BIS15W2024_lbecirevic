---
title: "lab 6 warmup"
output: 
  html_document: 
    keep_md: yes
date: "2024-01-30"
---




```r
library("tidyverse")
```

```
## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
## ✔ dplyr     1.1.4     ✔ readr     2.1.4
## ✔ forcats   1.0.0     ✔ stringr   1.5.1
## ✔ ggplot2   3.4.4     ✔ tibble    3.2.1
## ✔ lubridate 1.9.3     ✔ tidyr     1.3.0
## ✔ purrr     1.0.2     
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```

## Warm-up

### 1. Load the `bison.csv` data.


```r
bison <- read_csv("data/bison.csv")
```

```
## Rows: 8325 Columns: 8
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (3): data_code, animal_code, animal_sex
## dbl (5): rec_year, rec_month, rec_day, animal_weight, animal_yob
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

### 2. What are the dimesions and structure of the data?


```r
dim(bison)
```

```
## [1] 8325    8
```


```r
str(bison)
```

```
## spc_tbl_ [8,325 × 8] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ data_code    : chr [1:8325] "CBH01" "CBH01" "CBH01" "CBH01" ...
##  $ rec_year     : num [1:8325] 1994 1994 1994 1994 1994 ...
##  $ rec_month    : num [1:8325] 11 11 11 11 11 11 11 11 11 11 ...
##  $ rec_day      : num [1:8325] 8 8 8 8 8 8 8 8 8 8 ...
##  $ animal_code  : chr [1:8325] "813" "834" "B-301" "B-402" ...
##  $ animal_sex   : chr [1:8325] "F" "F" "F" "F" ...
##  $ animal_weight: num [1:8325] 890 1074 1060 989 1062 ...
##  $ animal_yob   : num [1:8325] 1981 1983 1983 1984 1984 ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   data_code = col_character(),
##   ..   rec_year = col_double(),
##   ..   rec_month = col_double(),
##   ..   rec_day = col_double(),
##   ..   animal_code = col_character(),
##   ..   animal_sex = col_character(),
##   ..   animal_weight = col_double(),
##   ..   animal_yob = col_double()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

### 3. We are only interested in code, sex, weight, year of birth. Restrict the data to these variables and store the dataframe as a new object.


```r
names(bison)
```

```
## [1] "data_code"     "rec_year"      "rec_month"     "rec_day"      
## [5] "animal_code"   "animal_sex"    "animal_weight" "animal_yob"
```


```r
bison_new <- bison %>% 
  select("data_code", "animal_sex", "animal_weight", "animal_yob")
```

### 4. Pull out the animals born between 1980-1990.


```r
bison_new%>% 
  filter(between(animal_yob, 1980, 1990))
```

```
## # A tibble: 435 × 4
##    data_code animal_sex animal_weight animal_yob
##    <chr>     <chr>              <dbl>      <dbl>
##  1 CBH01     F                    890       1981
##  2 CBH01     F                   1074       1983
##  3 CBH01     F                   1060       1983
##  4 CBH01     F                    989       1984
##  5 CBH01     F                   1062       1984
##  6 CBH01     F                    978       1985
##  7 CBH01     F                   1068       1985
##  8 CBH01     F                   1024       1985
##  9 CBH01     F                    978       1986
## 10 CBH01     F                   1188       1986
## # ℹ 425 more rows
```


```r
bison_new %>% 
  filter(animal_yob>=1980 & animal_yob<=1990)
```

```
## # A tibble: 435 × 4
##    data_code animal_sex animal_weight animal_yob
##    <chr>     <chr>              <dbl>      <dbl>
##  1 CBH01     F                    890       1981
##  2 CBH01     F                   1074       1983
##  3 CBH01     F                   1060       1983
##  4 CBH01     F                    989       1984
##  5 CBH01     F                   1062       1984
##  6 CBH01     F                    978       1985
##  7 CBH01     F                   1068       1985
##  8 CBH01     F                   1024       1985
##  9 CBH01     F                    978       1986
## 10 CBH01     F                   1188       1986
## # ℹ 425 more rows
```

### 5. How many male and female bison are represented between 1980-1990?


```r
males <- bison_new %>% 
  filter(between(animal_yob, 1980, 1990)) %>% 
  filter(animal_sex=="M")
```


```r
females <- bison_new %>% 
  filter(between(animal_yob, 1980, 1990)) %>% 
  filter(animal_sex=="F")
```


```r
table(males$animal_sex)
```

```
## 
##  M 
## 21
```

```r
table(females$animal_sex)
```

```
## 
##   F 
## 414
```

### 6. Between 1980-1990, were males or females larger on average?


```r
mean(males$animal_weight)
```

```
## [1] 1543.333
```

```r
mean(females$animal_weight)
```

```
## [1] 1017.314
```





