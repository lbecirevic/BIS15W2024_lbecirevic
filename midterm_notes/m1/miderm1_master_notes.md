---
title: "Midterm 1 Master Notes"
author: "Lejla Becirevic"
date: "2024-02-04"
output:
  html_document: 
    keep_md: true
  pdf_document: default
---




```r
library("tidyverse")
library("janitor")
library("skimr")
library("palmerpenguins")
```

## LAB 1
Github is a developer platform that allows people to create, store, manage and share their code.

**Check current working director**

```r
getwd()
```

```
## [1] "/Users/lbecirev/Desktop/BIS15W2024_lbecirevic/midterm_notes/m1"
```

**Making a vector and calculate mean, median, and standard deviation**

```r
x <- c(1, 2, 3, 4, 5)
```


```r
mean(x)
```

```
## [1] 3
```

```r
median(x)
```

```
## [1] 3
```

```r
sd(x)
```

```
## [1] 1.581139
```

## LAB 2
RStudio is a user interface for R that organizes the windows you see while using R. R markdown is text-based formatting that allows you to embed code and explanatory text in the same document. 

### Types of Data
There are five frequently used `classes` of data: 1. numeric, 2. integer, 3. character, 4. logical, 5. complex.

```r
my_numeric <- 42
my_integer <- 2L #adding an L automatically denotes an integer
my_character <- "universe"
my_logical <- FALSE
my_complex <- 2+4i
```

**Use class() to identify the type of data**

```r
class(my_numeric) #can also use $ to focus on specific column
```

```
## [1] "numeric"
```

**Use the is() to clarify and as() specify a type of data**

```r
is.integer(my_numeric) #is my_numeric an integer?
```

```
## [1] FALSE
```


```r
is.numeric(my_numeric)
```

```
## [1] TRUE
```


```r
my_integer <- 
  as.integer(my_numeric) #create a new object specified as an integer
```


```r
is.integer(my_integer) #is my_numeric an integer?
```

```
## [1] TRUE
```


```r
practice_integer <- 50L
is.integer(practice_integer)
```

```
## [1] TRUE
```


```r
practice_integer <- as.numeric(practice_integer)
is.integer(practice_integer)
```

```
## [1] FALSE
```

### NA 
**is.na() or anyNA() or na.rm=T are useful functions when dealing with NAs in data**

```r
my_missing <- NA
```


```r
is.na(my_missing)
```

```
## [1] TRUE
```


```r
anyNA(my_missing)
```

```
## [1] TRUE
```


```r
new_NA_practice <- c(10, NA, 20)
```


```r
is.na(new_NA_practice)
```

```
## [1] FALSE  TRUE FALSE
```


```r
anyNA(new_NA_practice)
```

```
## [1] TRUE
```


```r
new_vector <- c(7, 6.2, 5, 9, NA, 4, 9.8, 7, 3, 2)
mean(new_vector, na.rm=T) #na.rm removes the NA values in the vector
```

```
## [1] 5.888889
```

### Identifying vector elements

```r
my_vector <- c(10, 20, 30)
days_of_the_week <- c("Monday", "Tuesday", "Wednesday", "Thrusday", "Friday", "Saturday", "Sunday")
my_vector_sequence <- c(1:100)
```

**Use `[]` to only get the values and < (less than), > (more than), ==, <=, >=**

```r
days_of_the_week[4]
```

```
## [1] "Thrusday"
```

```r
my_vector_sequence[10]
```

```
## [1] 10
```

```r
my_vector_sequence==15
```

```
##   [1] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [13] FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [25] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [37] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [49] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [61] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [73] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [85] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [97] FALSE FALSE FALSE FALSE
```

```r
my_vector_sequence<=10 
```

```
##   [1]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [13] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [25] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [37] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [49] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [61] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [73] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [85] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [97] FALSE FALSE FALSE FALSE
```

```r
my_vector_sequence[my_vector_sequence<=10] 
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10
```

### Data Matrices

```r
Philosophers_Stone <- c(317.5, 657.1)
Chamber_of_Secrets <- c(261.9, 616.9)
Prisoner_of_Azkaban <- c(249.5, 547.1)
Goblet_of_Fire <- c(290.0, 606.8)
Order_of_the_Phoenix <- c(292.0, 647.8)
Half_Blood_Prince <- c(301.9, 632.4)
Deathly_Hallows_1 <- c(295.9, 664.3)
Deathly_Hallows_2 <- c(381.0, 960.5)
```


```r
box_office <- c(Philosophers_Stone, Chamber_of_Secrets, Prisoner_of_Azkaban, Goblet_of_Fire, Order_of_the_Phoenix, Half_Blood_Prince, Deathly_Hallows_1, Deathly_Hallows_2)
```

**Using the `matrix()` command and the `nrow` and `byrow` commands.**

```r
harry_potter_matrix <- matrix(box_office, nrow = 8, byrow = T)
```

**Name the rows and columns**

```r
region <- c("US", "non-US")
titles <- c("Philosophers_Stone", "Chamber_of_Secrets", "Prisoner_of_Azkaban", "Goblet_of_Fire", "Order_of_the_Phoenix", "Half_Blood_Prince", "Deathly_Hallows_1", "Deathly_Hallows_2")
```

**Name the columns using `colnames()` with the vector region**

```r
colnames(harry_potter_matrix) <- region
```

**Name the rows using `rownames()` with the vector titles**

```r
rownames(harry_potter_matrix) <- titles
```

**Print `harry_potter_matrix`**

```r
harry_potter_matrix
```

```
##                         US non-US
## Philosophers_Stone   317.5  657.1
## Chamber_of_Secrets   261.9  616.9
## Prisoner_of_Azkaban  249.5  547.1
## Goblet_of_Fire       290.0  606.8
## Order_of_the_Phoenix 292.0  647.8
## Half_Blood_Prince    301.9  632.4
## Deathly_Hallows_1    295.9  664.3
## Deathly_Hallows_2    381.0  960.5
```

**Using a data matrix**

```r
global <- rowSums(harry_potter_matrix)
```

**Use `cbind()` to adds columns**

```r
all_harry_potter_matrix <- cbind(harry_potter_matrix, global) #can also use rbind for rows
```


```r
all_harry_potter_matrix
```

```
##                         US non-US global
## Philosophers_Stone   317.5  657.1  974.6
## Chamber_of_Secrets   261.9  616.9  878.8
## Prisoner_of_Azkaban  249.5  547.1  796.6
## Goblet_of_Fire       290.0  606.8  896.8
## Order_of_the_Phoenix 292.0  647.8  939.8
## Half_Blood_Prince    301.9  632.4  934.3
## Deathly_Hallows_1    295.9  664.3  960.2
## Deathly_Hallows_2    381.0  960.5 1341.5
```

**The following selects the value in the first column, second row**

```r
harry_potter_matrix[2,1] #can also use for characters
```

```
## [1] 261.9
```

**Adding a colon `:` selects the specified elements in a column**

```r
harry_potter_matrix[1:4]
```

```
## [1] 317.5 261.9 249.5 290.0
```

**Select values in an entire row or column**

```r
non_us_earnings <- all_harry_potter_matrix[ ,2]
mean(non_us_earnings)
```

```
## [1] 666.6125
```

**Full example**

```r
plant_height <- c(30.7, 37.6, 28.4, NA, 33.2)
plant_weight <- c(4, 5.2, 3.7, NA, 4.6)
samples <- c("plant1", "plant2", "plant3", "plant4", "plant5")
measured <- c("height", "weight")
plant_experiment <- c(plant_height, plant_weight)
plant_experiment_matrix <- matrix(plant_experiment, nrow = 5, byrow = F)
colnames(plant_experiment_matrix) <- measured
rownames(plant_experiment_matrix) <- samples
plant_means <- colMeans(plant_experiment_matrix, na.rm=T)
plant_experiment_matrix_final <- rbind(plant_experiment_matrix, plant_means)
plant_experiment_matrix_final
```

```
##             height weight
## plant1      30.700  4.000
## plant2      37.600  5.200
## plant3      28.400  3.700
## plant4          NA     NA
## plant5      33.200  4.600
## plant_means 32.475  4.375
```

## LAB 3
A vector is a linear array of quantities. A matrix is a 2-dimensional array of quantities.

### Data Frames

```r
Sex <- c("male", "female", "male")
Length <- c(3.2, 3.7, 3.4)
Weight <- c(2.9, 4.0, 3.1)
```

**Create a data frame with the function `data.frame()`**

```r
hbirds <- data.frame(sex=Sex, length=Length, weight=Weight)
hbirds
```

```
##      sex length weight
## 1   male    3.2    2.9
## 2 female    3.7    4.0
## 3   male    3.4    3.1
```

**The column names of our data frame**

```r
names(hbirds) 
```

```
## [1] "sex"    "length" "weight"
```

**The `dim()` and `str()` commands provide the dimension of the dataframe** 

```r
dim(hbirds)
```

```
## [1] 3 3
```


```r
str(hbirds)
```

```
## 'data.frame':	3 obs. of  3 variables:
##  $ sex   : chr  "male" "female" "male"
##  $ length: num  3.2 3.7 3.4
##  $ weight: num  2.9 4 3.1
```

**Use lowercase names when we create the data frame**

```r
hbirds <- data.frame(sex=Sex, length=Length, weight_g=Weight)
```


```r
hbirds
```

```
##      sex length weight_g
## 1   male    3.2      2.9
## 2 female    3.7      4.0
## 3   male    3.4      3.1
```

### Accessing Data Frame Columns and Rows 
**The first row**

```r
hbirds[1,]
```

```
##    sex length weight_g
## 1 male    3.2      2.9
```

**The third column** 

```r
hbirds[ ,3]
```

```
## [1] 2.9 4.0 3.1
```

**Select values in an entire column using the `$` sign**

```r
w <- hbirds$weight_g
mean(w)
```

```
## [1] 3.333333
```

### Writing Data to File
**Here we write our data frame to a csv file. We use `row.names = FALSE` to avoid row numbers from printing out**

```r
write.csv(hbirds, "hbirds_data.csv", row.names = FALSE) #comma separated value
```

### Loading the data from files

```r
hot_springs <- read_csv("/Users/lbecirev/Desktop/BIS15W2024_lbecirevic/lab3/hsprings_data.csv")
```

```
## Rows: 9 Columns: 4
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (2): scientist, spring
## dbl (2): temp_C, depth_ft
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

**Count the number of rows and number of columns**

```r
nrow(hot_springs)
```

```
## [1] 9
```

```r
ncol(hot_springs)
```

```
## [1] 4
```

**`head()` prints the first n rows of the data frame**

```r
head(hot_springs)
```

```
## # A tibble: 6 × 4
##   temp_C scientist spring  depth_ft
##    <dbl> <chr>     <chr>      <dbl>
## 1   36.2 Jill      Buckeye     4.15
## 2   35.4 Susan     Buckeye     4.13
## 3   35.3 Steve     Buckeye     4.12
## 4   35.2 Jill      Benton      3.21
## 5   35.4 Susan     Benton      3.23
## 6   33.4 Steve     Benton      3.2
```

**`tail()` prints the last n rows of the data frame**

```r
tail(hot_springs)
```

```
## # A tibble: 6 × 4
##   temp_C scientist spring     depth_ft
##    <dbl> <chr>     <chr>         <dbl>
## 1   35.2 Jill      Benton         3.21
## 2   35.4 Susan     Benton         3.23
## 3   33.4 Steve     Benton         3.2 
## 4   30.7 Jill      Travertine     5.67
## 5   29.6 Susan     Travertine     5.65
## 6   29.2 Steve     Travertine     5.66
```

**`table()` is useful when you have a limited number of categorical variables**

```r
table(hot_springs$spring)
```

```
## 
##     Benton    Buckeye Travertine 
##          3          3          3
```


```r
#View(hot_springs)
```

**Replace scientists in hot_springs data with scientists as factor. Factor is when you have repeated sets of a specific type, not un-limitless**

```r
hot_springs$scientist <- as.factor(hot_springs$scientist)
hot_springs$spring <- as.factor(hot_springs$spring)
```
 
**Levels tell you how many factors you have in a category**

```r
levels(hot_springs$scientist)
```

```
## [1] "Jill"  "Steve" "Susan"
```

```r
levels(hot_springs$spring)
```

```
## [1] "Benton"     "Buckeye"    "Travertine"
```

## LAB 4
Data matrix has one class of data and a data frame have multiple classes of data.
**Every variable in its own column and every observation is in its own row and each cell had one value = tidy data (lab4_1**

### Load the data

```r
fish <- readr::read_csv("data/Gaeta_etal_CLC_data.csv") #readr means read package
```

```
## Rows: 4033 Columns: 6
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (2): lakeid, annnumber
## dbl (4): fish_id, length, radii_length_mm, scalelength
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


```r
mammals <- read_csv("data/mammal_lifehistories_v2.csv")
```

```
## Rows: 1440 Columns: 13
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (4): order, family, Genus, species
## dbl (9): mass, gestation, newborn, weaning, wean mass, AFR, max. life, litte...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

### dplyr
The first package that we will use that is part of the tidyverse is `dplyr`. `dplyr` is used to transform data frames by extracting, rearranging, and summarizing data such that they are focused on a question of interest. This is very helpful,  especially when wrangling large data, and makes dplyr one of most frequently used packages in the tidyverse. The two functions we will use most are `select()` and `filter()`.  

### select 
**Allows you to pull out columns of interest from a dataframe**

```r
select(fish, "lakeid", "scalelength") #The function is select(name of data frame, then variables of interest). Note: fish is an object
```

```
## # A tibble: 4,033 × 2
##    lakeid scalelength
##    <chr>        <dbl>
##  1 AL            2.70
##  2 AL            2.70
##  3 AL            2.70
##  4 AL            3.02
##  5 AL            3.02
##  6 AL            3.02
##  7 AL            3.02
##  8 AL            3.34
##  9 AL            3.34
## 10 AL            3.34
## # ℹ 4,023 more rows
```

**To add a range of columns use `start_col:end_col`**

```r
select(fish, fish_id:length)
```

```
## # A tibble: 4,033 × 3
##    fish_id annnumber length
##      <dbl> <chr>      <dbl>
##  1     299 EDGE         167
##  2     299 2            167
##  3     299 1            167
##  4     300 EDGE         175
##  5     300 3            175
##  6     300 2            175
##  7     300 1            175
##  8     301 EDGE         194
##  9     301 3            194
## 10     301 2            194
## # ℹ 4,023 more rows
```

**The - operator allows us to select everything except the specified variables**

```r
select(fish, -"fish_id", -"annnumber", -"length", -"radii_length_mm") #Use minus operator (-), remove variables you don't want
```

```
## # A tibble: 4,033 × 2
##    lakeid scalelength
##    <chr>        <dbl>
##  1 AL            2.70
##  2 AL            2.70
##  3 AL            2.70
##  4 AL            3.02
##  5 AL            3.02
##  6 AL            3.02
##  7 AL            3.02
##  8 AL            3.34
##  9 AL            3.34
## 10 AL            3.34
## # ℹ 4,023 more rows
```

Options to select columns based on a specific criteria include:  
1. ends_with() = Select columns that end with a character string  
2. contains() = Select columns that contain a character string  
3. matches() = Select columns that match a regular expression  
4. one_of() = Select columns names that are from a group of names


```r
select(fish, contains("length")) #Look into fish data and pull all variables with something to do with length
```

```
## # A tibble: 4,033 × 3
##    length radii_length_mm scalelength
##     <dbl>           <dbl>       <dbl>
##  1    167            2.70        2.70
##  2    167            2.04        2.70
##  3    167            1.31        2.70
##  4    175            3.02        3.02
##  5    175            2.67        3.02
##  6    175            2.14        3.02
##  7    175            1.23        3.02
##  8    194            3.34        3.34
##  9    194            2.97        3.34
## 10    194            2.29        3.34
## # ℹ 4,023 more rows
```


```r
select(fish, starts_with("radii")) #Pull out all the variables that starts_with or ends_with
```

```
## # A tibble: 4,033 × 1
##    radii_length_mm
##              <dbl>
##  1            2.70
##  2            2.04
##  3            1.31
##  4            3.02
##  5            2.67
##  6            2.14
##  7            1.23
##  8            3.34
##  9            2.97
## 10            2.29
## # ℹ 4,023 more rows
```


```r
select(fish, ends_with("id"))
```

```
## # A tibble: 4,033 × 2
##    lakeid fish_id
##    <chr>    <dbl>
##  1 AL         299
##  2 AL         299
##  3 AL         299
##  4 AL         300
##  5 AL         300
##  6 AL         300
##  7 AL         300
##  8 AL         301
##  9 AL         301
## 10 AL         301
## # ℹ 4,023 more rows
```


```r
select(fish, matches("a.+er")) #Handy bit of code for project; look at variables of interest with "a" and ends with "er"
```

```
## # A tibble: 4,033 × 1
##    annnumber
##    <chr>    
##  1 EDGE     
##  2 2        
##  3 1        
##  4 EDGE     
##  5 3        
##  6 2        
##  7 1        
##  8 EDGE     
##  9 3        
## 10 2        
## # ℹ 4,023 more rows
```


```r
select_if(fish, is.numeric) #pull all numerics
```

```
## # A tibble: 4,033 × 4
##    fish_id length radii_length_mm scalelength
##      <dbl>  <dbl>           <dbl>       <dbl>
##  1     299    167            2.70        2.70
##  2     299    167            2.04        2.70
##  3     299    167            1.31        2.70
##  4     300    175            3.02        3.02
##  5     300    175            2.67        3.02
##  6     300    175            2.14        3.02
##  7     300    175            1.23        3.02
##  8     301    194            3.34        3.34
##  9     301    194            2.97        3.34
## 10     301    194            2.29        3.34
## # ℹ 4,023 more rows
```

```r
select_if(mammals, ~is.character(.)) #pull all characters
```

```
## # A tibble: 1,440 × 4
##    order        family         Genus       species      
##    <chr>        <chr>          <chr>       <chr>        
##  1 Artiodactyla Antilocapridae Antilocapra americana    
##  2 Artiodactyla Bovidae        Addax       nasomaculatus
##  3 Artiodactyla Bovidae        Aepyceros   melampus     
##  4 Artiodactyla Bovidae        Alcelaphus  buselaphus   
##  5 Artiodactyla Bovidae        Ammodorcas  clarkei      
##  6 Artiodactyla Bovidae        Ammotragus  lervia       
##  7 Artiodactyla Bovidae        Antidorcas  marsupialis  
##  8 Artiodactyla Bovidae        Antilope    cervicapra   
##  9 Artiodactyla Bovidae        Bison       bison        
## 10 Artiodactyla Bovidae        Bison       bonasus      
## # ℹ 1,430 more rows
```

```r
select_if(mammals, is.character)
```

```
## # A tibble: 1,440 × 4
##    order        family         Genus       species      
##    <chr>        <chr>          <chr>       <chr>        
##  1 Artiodactyla Antilocapridae Antilocapra americana    
##  2 Artiodactyla Bovidae        Addax       nasomaculatus
##  3 Artiodactyla Bovidae        Aepyceros   melampus     
##  4 Artiodactyla Bovidae        Alcelaphus  buselaphus   
##  5 Artiodactyla Bovidae        Ammodorcas  clarkei      
##  6 Artiodactyla Bovidae        Ammotragus  lervia       
##  7 Artiodactyla Bovidae        Antidorcas  marsupialis  
##  8 Artiodactyla Bovidae        Antilope    cervicapra   
##  9 Artiodactyla Bovidae        Bison       bison        
## 10 Artiodactyla Bovidae        Bison       bonasus      
## # ℹ 1,430 more rows
```

**To select all columns that are *not* a class of data, you need to add a `~`.**

```r
select_if(fish, ~!is.numeric(.)) #Look across (~) into fish data and don't pull out numeric (! = not)
```

```
## # A tibble: 4,033 × 2
##    lakeid annnumber
##    <chr>  <chr>    
##  1 AL     EDGE     
##  2 AL     2        
##  3 AL     1        
##  4 AL     EDGE     
##  5 AL     3        
##  6 AL     2        
##  7 AL     1        
##  8 AL     EDGE     
##  9 AL     3        
## 10 AL     2        
## # ℹ 4,023 more rows
```

### Other
**Imported data frames often have a mix of lower and uppercase column names. Use `toupper()` or `tolower()` to fix this issue**

```r
select_all(mammals, tolower)
```

```
## # A tibble: 1,440 × 13
##    order       family genus species   mass gestation newborn weaning `wean mass`
##    <chr>       <chr>  <chr> <chr>    <dbl>     <dbl>   <dbl>   <dbl>       <dbl>
##  1 Artiodacty… Antil… Anti… americ… 4.54e4      8.13   3246.    3           8900
##  2 Artiodacty… Bovid… Addax nasoma… 1.82e5      9.39   5480     6.5         -999
##  3 Artiodacty… Bovid… Aepy… melamp… 4.15e4      6.35   5093     5.63       15900
##  4 Artiodacty… Bovid… Alce… busela… 1.5 e5      7.9   10167.    6.5         -999
##  5 Artiodacty… Bovid… Ammo… clarkei 2.85e4      6.8    -999  -999           -999
##  6 Artiodacty… Bovid… Ammo… lervia  5.55e4      5.08   3810     4           -999
##  7 Artiodacty… Bovid… Anti… marsup… 3   e4      5.72   3910     4.04        -999
##  8 Artiodacty… Bovid… Anti… cervic… 3.75e4      5.5    3846     2.13        -999
##  9 Artiodacty… Bovid… Bison bison   4.98e5      8.93  20000    10.7       157500
## 10 Artiodacty… Bovid… Bison bonasus 5   e5      9.14  23000.    6.6         -999
## # ℹ 1,430 more rows
## # ℹ 4 more variables: afr <dbl>, `max. life` <dbl>, `litter size` <dbl>,
## #   `litters/year` <dbl>
```


```r
clean_names(mammals) #janitor package
```

```
## # A tibble: 1,440 × 13
##    order  family genus species   mass gestation newborn weaning wean_mass    afr
##    <chr>  <chr>  <chr> <chr>    <dbl>     <dbl>   <dbl>   <dbl>     <dbl>  <dbl>
##  1 Artio… Antil… Anti… americ… 4.54e4      8.13   3246.    3         8900   13.5
##  2 Artio… Bovid… Addax nasoma… 1.82e5      9.39   5480     6.5       -999   27.3
##  3 Artio… Bovid… Aepy… melamp… 4.15e4      6.35   5093     5.63     15900   16.7
##  4 Artio… Bovid… Alce… busela… 1.5 e5      7.9   10167.    6.5       -999   23.0
##  5 Artio… Bovid… Ammo… clarkei 2.85e4      6.8    -999  -999         -999 -999  
##  6 Artio… Bovid… Ammo… lervia  5.55e4      5.08   3810     4         -999   14.9
##  7 Artio… Bovid… Anti… marsup… 3   e4      5.72   3910     4.04      -999   10.2
##  8 Artio… Bovid… Anti… cervic… 3.75e4      5.5    3846     2.13      -999   20.1
##  9 Artio… Bovid… Bison bison   4.98e5      8.93  20000    10.7     157500   29.4
## 10 Artio… Bovid… Bison bonasus 5   e5      9.14  23000.    6.6       -999   30.0
## # ℹ 1,430 more rows
## # ℹ 3 more variables: max_life <dbl>, litter_size <dbl>, litters_year <dbl>
```

**When naming columns, blank spaces are often added (don't do this, please). Here is a trick to remove these**

```r
#select_all(mammals, ~str_replace(., " ", "_"))
```



### filter
**`filter()` allows us to extract data that meet specific criteria within a variable**

```r
filter(fish, lakeid == "AL") #Look in fish data and pull out all observations that correspond with lakeid "AL" Note: needs to be two equal signs (==)
```

```
## # A tibble: 383 × 6
##    lakeid fish_id annnumber length radii_length_mm scalelength
##    <chr>    <dbl> <chr>      <dbl>           <dbl>       <dbl>
##  1 AL         299 EDGE         167            2.70        2.70
##  2 AL         299 2            167            2.04        2.70
##  3 AL         299 1            167            1.31        2.70
##  4 AL         300 EDGE         175            3.02        3.02
##  5 AL         300 3            175            2.67        3.02
##  6 AL         300 2            175            2.14        3.02
##  7 AL         300 1            175            1.23        3.02
##  8 AL         301 EDGE         194            3.34        3.34
##  9 AL         301 3            194            2.97        3.34
## 10 AL         301 2            194            2.29        3.34
## # ℹ 373 more rows
```


```r
filter(fish, length >= 350)
```

```
## # A tibble: 890 × 6
##    lakeid fish_id annnumber length radii_length_mm scalelength
##    <chr>    <dbl> <chr>      <dbl>           <dbl>       <dbl>
##  1 AL         306 EDGE         350            6.94        6.94
##  2 AL         306 10           350            6.46        6.94
##  3 AL         306 9            350            6.16        6.94
##  4 AL         306 8            350            5.88        6.94
##  5 AL         306 7            350            5.42        6.94
##  6 AL         306 6            350            4.90        6.94
##  7 AL         306 5            350            4.46        6.94
##  8 AL         306 4            350            3.75        6.94
##  9 AL         306 3            350            2.93        6.94
## 10 AL         306 2            350            2.14        6.94
## # ℹ 880 more rows
```

**>, >=, <, <=, != (not equal), and == (equal)** 

**`!` operator allows for the exclusion of specific observations**

```r
not_AL <- filter(fish, lakeid != "AL") #Pull out all fish not "AL" 
```

**Filtering multiple values within the same variable requires the `%in%`**   

```r
filter(fish, length %in% c(167, 175)) #Pull out all the fish within the length 167 to 175 (%in%); for multiple values within dataset
```

```
## # A tibble: 18 × 6
##    lakeid fish_id annnumber length radii_length_mm scalelength
##    <chr>    <dbl> <chr>      <dbl>           <dbl>       <dbl>
##  1 AL         299 EDGE         167           2.70         2.70
##  2 AL         299 2            167           2.04         2.70
##  3 AL         299 1            167           1.31         2.70
##  4 AL         300 EDGE         175           3.02         3.02
##  5 AL         300 3            175           2.67         3.02
##  6 AL         300 2            175           2.14         3.02
##  7 AL         300 1            175           1.23         3.02
##  8 BO         397 EDGE         175           2.67         2.67
##  9 BO         397 3            175           2.39         2.67
## 10 BO         397 2            175           1.59         2.67
## 11 BO         397 1            175           0.830        2.67
## 12 LSG         45 EDGE         175           3.21         3.21
## 13 LSG         45 3            175           2.92         3.21
## 14 LSG         45 2            175           2.44         3.21
## 15 LSG         45 1            175           1.60         3.21
## 16 RD         103 EDGE         167           2.80         2.80
## 17 RD         103 2            167           2.10         2.80
## 18 RD         103 1            167           1.31         2.80
```

**Alternatively, you can use `between` if you are looking for a range of specific values**

```r
filter(fish, between(scalelength, 2.5, 2.55)) #Pull fish with scale length of 2.5 and 2.55
```

```
## # A tibble: 10 × 6
##    lakeid fish_id annnumber length radii_length_mm scalelength
##    <chr>    <dbl> <chr>      <dbl>           <dbl>       <dbl>
##  1 LSG         56 EDGE         145            2.55        2.55
##  2 LSG         56 2            145            1.94        2.55
##  3 LSG         56 1            145            1.20        2.55
##  4 LSG         57 EDGE         143            2.52        2.52
##  5 LSG         57 2            143            2.13        2.52
##  6 LSG         57 1            143            1.19        2.52
##  7 UB          80 EDGE         153            2.55        2.55
##  8 UB          80 3            153            2.10        2.55
##  9 UB          80 2            153            1.62        2.55
## 10 UB          80 1            153            1.14        2.55
```

**You can also extract observations "near" a certain value but you need to specify a tolerance**

```r
filter(fish, near(radii_length_mm, 2, tol = 0.2)) #Pull data near a certain value, near 2 within 0.2 tolerance 
```

```
## # A tibble: 291 × 6
##    lakeid fish_id annnumber length radii_length_mm scalelength
##    <chr>    <dbl> <chr>      <dbl>           <dbl>       <dbl>
##  1 AL         299 2            167            2.04        2.70
##  2 AL         300 2            175            2.14        3.02
##  3 AL         302 2            324            2.19        6.07
##  4 AL         303 2            325            2.04        6.79
##  5 AL         306 2            350            2.14        6.94
##  6 AL         308 2            355            1.86        6.67
##  7 AL         312 2            367            2.17        6.81
##  8 AL         313 2            367            2.06        6.47
##  9 AL         315 2            372            2.04        6.47
## 10 AL         316 2            372            1.82        6.35
## # ℹ 281 more rows
```

**Use `filter()` to extract data based on multiple conditions. Below we extract only the fish that have lakeid "AL" and length >350**

```r
filter(fish, lakeid == "AL" & length > 350) #"And" filter = exclusive
```

```
## # A tibble: 314 × 6
##    lakeid fish_id annnumber length radii_length_mm scalelength
##    <chr>    <dbl> <chr>      <dbl>           <dbl>       <dbl>
##  1 AL         307 EDGE         353            7.55        7.55
##  2 AL         307 13           353            7.28        7.55
##  3 AL         307 12           353            6.98        7.55
##  4 AL         307 11           353            6.73        7.55
##  5 AL         307 10           353            6.48        7.55
##  6 AL         307 9            353            6.22        7.55
##  7 AL         307 8            353            5.92        7.55
##  8 AL         307 7            353            5.44        7.55
##  9 AL         307 6            353            5.06        7.55
## 10 AL         307 5            353            4.37        7.55
## # ℹ 304 more rows
```

**Notice that the `|` operator generates a different result**

```r
filter(fish, lakeid == "AL" | length > 350) #Stands for "or" = inclusive
```

```
## # A tibble: 948 × 6
##    lakeid fish_id annnumber length radii_length_mm scalelength
##    <chr>    <dbl> <chr>      <dbl>           <dbl>       <dbl>
##  1 AL         299 EDGE         167            2.70        2.70
##  2 AL         299 2            167            2.04        2.70
##  3 AL         299 1            167            1.31        2.70
##  4 AL         300 EDGE         175            3.02        3.02
##  5 AL         300 3            175            2.67        3.02
##  6 AL         300 2            175            2.14        3.02
##  7 AL         300 1            175            1.23        3.02
##  8 AL         301 EDGE         194            3.34        3.34
##  9 AL         301 3            194            2.97        3.34
## 10 AL         301 2            194            2.29        3.34
## # ℹ 938 more rows
```

**In this case, we filter out the fish with a length over 400 and a scale length over 11 or a radii length over 8**

```r
filter(fish, length > 400, (scalelength > 11 | radii_length_mm > 8))
```

```
## # A tibble: 23 × 6
##    lakeid fish_id annnumber length radii_length_mm scalelength
##    <chr>    <dbl> <chr>      <dbl>           <dbl>       <dbl>
##  1 AL         324 EDGE         406            8.21        8.21
##  2 AL         327 EDGE         413            8.33        8.33
##  3 AL         327 15           413            8.11        8.33
##  4 AL         328 EDGE         420            8.71        8.71
##  5 AL         328 16           420            8.41        8.71
##  6 AL         328 15           420            8.14        8.71
##  7 WS         180 EDGE         403           11.0        11.0 
##  8 WS         180 16           403           10.6        11.0 
##  9 WS         180 15           403           10.3        11.0 
## 10 WS         180 14           403            9.93       11.0 
## # ℹ 13 more rows
```

### Filter Rules 
+ `filter(condition1, condition2)` will return rows where both conditions are met.  
+ `filter(condition1, !condition2)` will return all rows where condition one is true but condition 2 is not.  
+ `filter(condition1 | condition2)` will return rows where condition 1 or condition 2 is met.  
+ `filter(xor(condition1, condition2)` will return all rows where only one of the conditions is met, and not when both conditions are met.  

**Load the data into a new object called `homerange`.**

```r
homerange <- read_csv("data/Tamburelloetal_HomeRangeDatabase.csv")
```

```
## Rows: 569 Columns: 24
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (16): taxon, common.name, class, order, family, genus, species, primarym...
## dbl  (8): mean.mass.g, log10.mass, mean.hra.m2, log10.hra, dimension, preyma...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

**Change the class of the variables `taxon` and `order` to factors and display their levels**  

```r
homerange$taxon <- as.factor(homerange$taxon)
levels(homerange$taxon)
```

```
## [1] "birds"         "lake fishes"   "lizards"       "mammals"      
## [5] "marine fishes" "river fishes"  "snakes"        "tortoises"    
## [9] "turtles"
```


```r
homerange$order <- as.factor(homerange$order)
levels(homerange$order)
```

```
##  [1] "accipitriformes"       "afrosoricida"          "anguilliformes"       
##  [4] "anseriformes"          "apterygiformes"        "artiodactyla"         
##  [7] "caprimulgiformes"      "carnivora"             "charadriiformes"      
## [10] "columbidormes"         "columbiformes"         "coraciiformes"        
## [13] "cuculiformes"          "cypriniformes"         "dasyuromorpha"        
## [16] "dasyuromorpia"         "didelphimorphia"       "diprodontia"          
## [19] "diprotodontia"         "erinaceomorpha"        "esociformes"          
## [22] "falconiformes"         "gadiformes"            "galliformes"          
## [25] "gruiformes"            "lagomorpha"            "macroscelidea"        
## [28] "monotrematae"          "passeriformes"         "pelecaniformes"       
## [31] "peramelemorphia"       "perciformes"           "perissodactyla"       
## [34] "piciformes"            "pilosa"                "proboscidea"          
## [37] "psittaciformes"        "rheiformes"            "roden"                
## [40] "rodentia"              "salmoniformes"         "scorpaeniformes"      
## [43] "siluriformes"          "soricomorpha"          "squamata"             
## [46] "strigiformes"          "struthioniformes"      "syngnathiformes"      
## [49] "testudines"            "tetraodontiformes\xa0" "tinamiformes"
```

**Example**

```r
owls <- filter(homerange, order=="strigiformes")
owls_data <- select(owls, "mean.mass.g", "log10.mass", "family", "genus", "species", "common.name")
filter(owls_data, mean.mass.g==61.32) 
```

```
## # A tibble: 1 × 6
##   mean.mass.g log10.mass family    genus      species    common.name       
##         <dbl>      <dbl> <chr>     <chr>      <chr>      <chr>             
## 1        61.3       1.79 strigidae glaucidium passerinum Eurasian pygmy owl
```

## LAB 5
Tidyverse is a library, dplyr is used to transform data, within dplyr filter and select are commands. Select is used to select variables (columns) of interest and filter is used to filter values (rows) of interest.

**Rename the variables**

```r
mammals <- rename(mammals, genus="Genus", wean_mass="wean mass", max_life= "max. life", litter_size="litter size", litters_per_year="litters/year")
```

### Pipes `%>%` 
**Start combining `select()`, `filter()`, and other functions. Pipes feed the output from one function into the input of another function. This helps us keep our code sequential and clean (Shift + command + m)**

```r
fish %>% #Work with the fish data 
  select(lakeid, radii_length_mm) %>% #Pull out variables of interest
  filter(lakeid=="AL" | lakeid=="AR") %>% #Only these lakes
  filter(between(radii_length_mm, 2, 4)) %>% #Between 2 and 4
  arrange(desc(radii_length_mm)) #Sort to make easier to read
```

```
## # A tibble: 253 × 2
##    lakeid radii_length_mm
##    <chr>            <dbl>
##  1 AR                4.00
##  2 AR                3.99
##  3 AR                3.99
##  4 AR                3.98
##  5 AR                3.98
##  6 AR                3.96
##  7 AR                3.94
##  8 AR                3.94
##  9 AR                3.94
## 10 AL                3.94
## # ℹ 243 more rows
```

**The `arrange()` command is default is ascending order**

```r
fish %>% 
  select(lakeid, scalelength) %>% 
  arrange(scalelength)
```

```
## # A tibble: 4,033 × 2
##    lakeid scalelength
##    <chr>        <dbl>
##  1 WS           0.628
##  2 WS           0.637
##  3 LSG          0.773
##  4 WS           0.832
##  5 LSG          1.15 
##  6 WS           1.41 
##  7 WS           1.41 
##  8 WS           1.41 
##  9 BO           1.43 
## 10 BO           1.43 
## # ℹ 4,023 more rows
```

**To sort in decreasing order, wrap the variable name in `desc()`**

```r
fish %>% 
  select(lakeid, scalelength) %>% 
  arrange(desc(scalelength))
```

```
## # A tibble: 4,033 × 2
##    lakeid scalelength
##    <chr>        <dbl>
##  1 WS            11.0
##  2 WS            11.0
##  3 WS            11.0
##  4 WS            11.0
##  5 WS            11.0
##  6 WS            11.0
##  7 WS            11.0
##  8 WS            11.0
##  9 WS            11.0
## 10 WS            11.0
## # ℹ 4,023 more rows
```


### mutate 
**Allows us to create a new column from existing columns in a data frame  

```r
fish %>% 
  mutate(length_mm = length*10) %>% 
  select(fish_id, length, length_mm)
```

```
## # A tibble: 4,033 × 3
##    fish_id length length_mm
##      <dbl>  <dbl>     <dbl>
##  1     299    167      1670
##  2     299    167      1670
##  3     299    167      1670
##  4     300    175      1750
##  5     300    175      1750
##  6     300    175      1750
##  7     300    175      1750
##  8     301    194      1940
##  9     301    194      1940
## 10     301    194      1940
## # ℹ 4,023 more rows
```

**`mutate_all()` is super helpful when cleaning data.** 

```r
mammals %>%
  mutate_all(tolower)
```

```
## # A tibble: 1,440 × 13
##    order    family genus species mass  gestation newborn weaning wean_mass AFR  
##    <chr>    <chr>  <chr> <chr>   <chr> <chr>     <chr>   <chr>   <chr>     <chr>
##  1 artioda… antil… anti… americ… 45375 8.13      3246.36 3       8900      13.53
##  2 artioda… bovid… addax nasoma… 1823… 9.39      5480    6.5     -999      27.27
##  3 artioda… bovid… aepy… melamp… 41480 6.35      5093    5.63    15900     16.66
##  4 artioda… bovid… alce… busela… 1500… 7.9       10166.… 6.5     -999      23.02
##  5 artioda… bovid… ammo… clarkei 28500 6.8       -999    -999    -999      -999 
##  6 artioda… bovid… ammo… lervia  55500 5.08      3810    4       -999      14.89
##  7 artioda… bovid… anti… marsup… 30000 5.72      3910    4.04    -999      10.23
##  8 artioda… bovid… anti… cervic… 37500 5.5       3846    2.13    -999      20.13
##  9 artioda… bovid… bison bison   4976… 8.93      20000   10.71   157500    29.45
## 10 artioda… bovid… bison bonasus 5e+05 9.14      23000.… 6.6     -999      29.99
## # ℹ 1,430 more rows
## # ℹ 3 more variables: max_life <chr>, litter_size <chr>, litters_per_year <chr>
```


```r
mammals %>% 
  mutate(across(c("order", "family"), tolower)) #use for changing names of specific variables
```

```
## # A tibble: 1,440 × 13
##    order  family genus species   mass gestation newborn weaning wean_mass    AFR
##    <chr>  <chr>  <chr> <chr>    <dbl>     <dbl>   <dbl>   <dbl>     <dbl>  <dbl>
##  1 artio… antil… Anti… americ… 4.54e4      8.13   3246.    3         8900   13.5
##  2 artio… bovid… Addax nasoma… 1.82e5      9.39   5480     6.5       -999   27.3
##  3 artio… bovid… Aepy… melamp… 4.15e4      6.35   5093     5.63     15900   16.7
##  4 artio… bovid… Alce… busela… 1.5 e5      7.9   10167.    6.5       -999   23.0
##  5 artio… bovid… Ammo… clarkei 2.85e4      6.8    -999  -999         -999 -999  
##  6 artio… bovid… Ammo… lervia  5.55e4      5.08   3810     4         -999   14.9
##  7 artio… bovid… Anti… marsup… 3   e4      5.72   3910     4.04      -999   10.2
##  8 artio… bovid… Anti… cervic… 3.75e4      5.5    3846     2.13      -999   20.1
##  9 artio… bovid… Bison bison   4.98e5      8.93  20000    10.7     157500   29.4
## 10 artio… bovid… Bison bonasus 5   e5      9.14  23000.    6.6       -999   30.0
## # ℹ 1,430 more rows
## # ℹ 3 more variables: max_life <dbl>, litter_size <dbl>, litters_per_year <dbl>
```

**`With `ifelse()`, you first specify a logical statement, afterwards what needs to happen if the statement returns `TRUE`, and lastly what needs to happen if it's  `FALSE`**

```r
mammals %>% 
  select(genus, species, newborn) %>% #select only these columns of interest
  mutate(newborn_new = ifelse(newborn == -999.00, NA, newborn))%>%  #replace those values with na, if else if newborn is -999.00 replace with na and if its not -999 leave it alone. always create a new variable to see changes
  arrange(newborn)
```

```
## # A tibble: 1,440 × 4
##    genus       species        newborn newborn_new
##    <chr>       <chr>            <dbl>       <dbl>
##  1 Ammodorcas  clarkei           -999          NA
##  2 Bos         javanicus         -999          NA
##  3 Bubalus     depressicornis    -999          NA
##  4 Bubalus     mindorensis       -999          NA
##  5 Capra       falconeri         -999          NA
##  6 Cephalophus niger             -999          NA
##  7 Cephalophus nigrifrons        -999          NA
##  8 Cephalophus natalensis        -999          NA
##  9 Cephalophus leucogaster       -999          NA
## 10 Cephalophus ogilbyi           -999          NA
## # ℹ 1,430 more rows
```

## LAB 6

```r
superhero_info <- read_csv("data/heroes_information.csv", na = c("", "-99", "-"))
```

```
## Rows: 734 Columns: 10
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (8): name, Gender, Eye color, Race, Hair color, Publisher, Skin color, A...
## dbl (2): Height, Weight
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
superhero_powers <- read_csv("data/super_hero_powers.csv", na = c("", "-99", "-"))
```

```
## Rows: 667 Columns: 168
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr   (1): hero_names
## lgl (167): Agility, Accelerated Healing, Lantern Power Ring, Dimensional Awa...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

**Data tidy**

```r
superhero_info <- clean_names(superhero_info)
superhero_powers <- clean_names(superhero_powers)
```

### tabyl
**The `janitor` package has its version of `table` which not only produces counts but also percentages**

```r
tabyl(superhero_info, alignment)
```

```
##  alignment   n     percent valid_percent
##        bad 207 0.282016349    0.28473177
##       good 496 0.675749319    0.68225585
##    neutral  24 0.032697548    0.03301238
##       <NA>   7 0.009536785            NA
```

**Highest height to weight ratio**  

```r
height_weight_ratio <- superhero_info %>% 
  select(name, height, weight)

height_weight_ratio %>% 
  mutate(ratio = height/weight) %>% 
  arrange(desc(ratio)) 
```

```
## # A tibble: 734 × 4
##    name            height weight  ratio
##    <chr>            <dbl>  <dbl>  <dbl>
##  1 Groot              701      4 175.  
##  2 Galactus           876     16  54.8 
##  3 Fin Fang Foom      975     18  54.2 
##  4 Longshot           188     36   5.22
##  5 Jack-Jack           71     14   5.07
##  6 Rocket Raccoon     122     25   4.88
##  7 Dash               122     27   4.52
##  8 Howard the Duck     79     18   4.39
##  9 Swarm              196     47   4.17
## 10 Yoda                66     17   3.88
## # ℹ 724 more rows
```

**Combination of multiple data**

```r
superhero_powers %>% 
  select(agility, stealth, super_strength, stamina) %>% 
  filter(agility==T) %>% 
  filter(stealth==T) %>% 
  filter(super_strength==T) %>% 
  filter(stamina==T) 
```

```
## # A tibble: 40 × 4
##    agility stealth super_strength stamina
##    <lgl>   <lgl>   <lgl>          <lgl>  
##  1 TRUE    TRUE    TRUE           TRUE   
##  2 TRUE    TRUE    TRUE           TRUE   
##  3 TRUE    TRUE    TRUE           TRUE   
##  4 TRUE    TRUE    TRUE           TRUE   
##  5 TRUE    TRUE    TRUE           TRUE   
##  6 TRUE    TRUE    TRUE           TRUE   
##  7 TRUE    TRUE    TRUE           TRUE   
##  8 TRUE    TRUE    TRUE           TRUE   
##  9 TRUE    TRUE    TRUE           TRUE   
## 10 TRUE    TRUE    TRUE           TRUE   
## # ℹ 30 more rows
```

## LAB 7

**msleep loaded in package**

```r
msleep <- msleep
```

### dplyr practice (exam question)
Let's do a bit more practice to make sure that we understand `select()`, `filter()`, and `mutate()`. Start by building a new data frame `msleep24` from the `msleep` data that: contains the `name` and `vore` variables along with a new column called `sleep_total_24` which is the amount of time a species sleeps expressed as a proportion of a 24-hour day. Restrict the `sleep_total_24` values to less than or equal to 0.3. Arrange the output in descending order.  

```r
msleep24 <- msleep %>% 
  mutate(sleep_total_24=sleep_total/24) %>% 
  select(name, vore, sleep_total_24, sleep_total) %>% 
  filter(sleep_total_24<=0.3) %>% 
  arrange(desc(sleep_total_24))
```

**`skim()` as part of the `skimr` package**

```r
skim(msleep24)
```


Table: Data summary

|                         |         |
|:------------------------|:--------|
|Name                     |msleep24 |
|Number of rows           |20       |
|Number of columns        |4        |
|_______________________  |         |
|Column type frequency:   |         |
|character                |2        |
|numeric                  |2        |
|________________________ |         |
|Group variables          |None     |


**Variable type: character**

|skim_variable | n_missing| complete_rate| min| max| empty| n_unique| whitespace|
|:-------------|---------:|-------------:|---:|---:|-----:|--------:|----------:|
|name          |         0|           1.0|   3|  20|     0|       20|          0|
|vore          |         2|           0.9|   5|   5|     0|        2|          0|


**Variable type: numeric**

|skim_variable  | n_missing| complete_rate| mean|   sd|   p0|  p25|  p50|  p75| p100|hist  |
|:--------------|---------:|-------------:|----:|----:|----:|----:|----:|----:|----:|:-----|
|sleep_total_24 |         0|             1| 0.19| 0.06| 0.08| 0.14| 0.17| 0.23| 0.29|▃▇▂▇▅ |
|sleep_total    |         0|             1| 4.46| 1.45| 1.90| 3.25| 4.20| 5.45| 7.00|▃▇▂▇▅ |

### summarize
**`summarize()` will produce summary statistics for a given variable in a data frame**

```r
head(msleep)
```

```
## # A tibble: 6 × 11
##   name    genus vore  order conservation sleep_total sleep_rem sleep_cycle awake
##   <chr>   <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl> <dbl>
## 1 Cheetah Acin… carni Carn… lc                  12.1      NA        NA      11.9
## 2 Owl mo… Aotus omni  Prim… <NA>                17         1.8      NA       7  
## 3 Mounta… Aplo… herbi Rode… nt                  14.4       2.4      NA       9.6
## 4 Greate… Blar… omni  Sori… lc                  14.9       2.3       0.133   9.1
## 5 Cow     Bos   herbi Arti… domesticated         4         0.7       0.667  20  
## 6 Three-… Brad… herbi Pilo… <NA>                14.4       2.2       0.767   9.6
## # ℹ 2 more variables: brainwt <dbl>, bodywt <dbl>
```

```r
large <- msleep %>% 
  select(name, genus, bodywt, sleep_total) %>% 
  filter(bodywt > 200) %>% 
  arrange(desc(bodywt))
```

**Can accomplish the same task using the `summarize()` function to make things cleaner**

```r
msleep %>% 
  filter(bodywt > 200) %>% 
  summarize(mean_sleep_lg=mean(sleep_total))
```

```
## # A tibble: 1 × 1
##   mean_sleep_lg
##           <dbl>
## 1           3.3
```


```r
msleep %>% 
  filter(bodywt < 10) %>% 
  summarize(sleep_total_sm=mean(sleep_total))
```

```
## # A tibble: 1 × 1
##   sleep_total_sm
##            <dbl>
## 1           12.0
```

**Combine functions to make useful summaries for multiple variables**

```r
msleep %>% 
  filter(bodywt>200) %>% 
  summarize(mean_sleep_lg=mean(sleep_total),
            min_sleep_lg=min(sleep_total),
            max_sleep_lg=max(sleep_total),
            sd_sleep_lg=sd(sleep_total),
            total=n()) #tells you the total number of observations, 7 animals total
```

```
## # A tibble: 1 × 5
##   mean_sleep_lg min_sleep_lg max_sleep_lg sd_sleep_lg total
##           <dbl>        <dbl>        <dbl>       <dbl> <int>
## 1           3.3          1.9          4.4       0.870     7
```

**Example:What is the mean, min, and max `bodywt` for the taxonomic order Primates? Provide the total number of observations.

```r
msleep %>% 
  filter(order=="Primates") %>% 
  summarize(mean_bodywt=mean(bodywt),
            min_bodywt=min(bodywt),
            max_bodywt=max(bodywt),
            total=n())
```

```
## # A tibble: 1 × 4
##   mean_bodywt min_bodywt max_bodywt total
##         <dbl>      <dbl>      <dbl> <int>
## 1        13.9        0.2         62    12
```

### n_distinct
**n_distinct() is a very handy way of cleanly presenting the number of distinct observations. Here we show the number of distinct genera over 100 in body weight**


```r
msleep %>% 
  filter(bodywt > 100) #Notice that there are multiple genera with over 100 in body weight.
```

```
## # A tibble: 11 × 11
##    name   genus vore  order conservation sleep_total sleep_rem sleep_cycle awake
##    <chr>  <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl> <dbl>
##  1 Cow    Bos   herbi Arti… domesticated         4         0.7       0.667  20  
##  2 Asian… Elep… herbi Prob… en                   3.9      NA        NA      20.1
##  3 Horse  Equus herbi Peri… domesticated         2.9       0.6       1      21.1
##  4 Donkey Equus herbi Peri… domesticated         3.1       0.4      NA      20.9
##  5 Giraf… Gira… herbi Arti… cd                   1.9       0.4      NA      22.1
##  6 Pilot… Glob… carni Ceta… cd                   2.7       0.1      NA      21.4
##  7 Afric… Loxo… herbi Prob… vu                   3.3      NA        NA      20.7
##  8 Tiger  Pant… carni Carn… en                  15.8      NA        NA       8.2
##  9 Lion   Pant… carni Carn… vu                  13.5      NA        NA      10.5
## 10 Brazi… Tapi… herbi Peri… vu                   4.4       1         0.9    19.6
## 11 Bottl… Turs… carni Ceta… <NA>                 5.2      NA        NA      18.8
## # ℹ 2 more variables: brainwt <dbl>, bodywt <dbl>
```


```r
msleep %>% 
  summarize(n_genera=n_distinct(genus)) #this is going to count the number of genera in msleep
```

```
## # A tibble: 1 × 1
##   n_genera
##      <int>
## 1       77
```

**There are many other useful summary statistics, depending on your needs: sd(), min(), max(), median(), sum(), n() (returns the length of a column), first() (returns first value in a column), last() (returns last value in a column) and n_distinct() (number of distinct values in a column)**

### group_by
**The `summarize()` function is most useful when used in conjunction with `group_by()`. Although producing a summary of body weight for all of the mammals in the data set is helpful, what if we were interested in body weight by feeding ecology?**

```r
msleep %>%
  group_by(vore) %>% #we are grouping by feeding ecology, a categorical variable
  summarize(min_bodywt = min(bodywt),
            max_bodywt = max(bodywt),
            mean_bodywt = mean(bodywt),
            total=n()) #group by and summarize work well together 
```

```
## # A tibble: 5 × 5
##   vore    min_bodywt max_bodywt mean_bodywt total
##   <chr>        <dbl>      <dbl>       <dbl> <int>
## 1 carni        0.028      800        90.8      19
## 2 herbi        0.022     6654       367.       32
## 3 insecti      0.01        60        12.9       5
## 4 omni         0.005       86.2      12.7      20
## 5 <NA>         0.021        3.6       0.858     7
```

**Example**
1. Calculate mean brain weight by taxonomic order in the msleep data.

```r
msleep %>% 
  group_by(order) %>% 
  summarize(mean_brain=mean(brainwt))
```

```
## # A tibble: 19 × 2
##    order           mean_brain
##    <chr>                <dbl>
##  1 Afrosoricida      0.0026  
##  2 Artiodactyla     NA       
##  3 Carnivora        NA       
##  4 Cetacea          NA       
##  5 Chiroptera        0.000275
##  6 Cingulata         0.0459  
##  7 Didelphimorphia  NA       
##  8 Diprotodontia    NA       
##  9 Erinaceomorpha    0.00295 
## 10 Hyracoidea        0.0152  
## 11 Lagomorpha        0.0121  
## 12 Monotremata       0.025   
## 13 Perissodactyla    0.414   
## 14 Pilosa           NA       
## 15 Primates         NA       
## 16 Proboscidea       5.16    
## 17 Rodentia         NA       
## 18 Scandentia        0.0025  
## 19 Soricomorpha      0.000592
```

2. Try running the code again, but this time add `na.rm=TRUE`. What is the problem with Cetacea? Compare this to Carnivora. 

```r
msleep %>% 
  group_by(order) %>% 
  summarize(mean_brain=mean(brainwt, na.rm = T)) #Cetacea has a NaN
```

```
## # A tibble: 19 × 2
##    order           mean_brain
##    <chr>                <dbl>
##  1 Afrosoricida      0.0026  
##  2 Artiodactyla      0.198   
##  3 Carnivora         0.0986  
##  4 Cetacea         NaN       
##  5 Chiroptera        0.000275
##  6 Cingulata         0.0459  
##  7 Didelphimorphia   0.0063  
##  8 Diprotodontia     0.0114  
##  9 Erinaceomorpha    0.00295 
## 10 Hyracoidea        0.0152  
## 11 Lagomorpha        0.0121  
## 12 Monotremata       0.025   
## 13 Perissodactyla    0.414   
## 14 Pilosa          NaN       
## 15 Primates          0.254   
## 16 Proboscidea       5.16    
## 17 Rodentia          0.00357 
## 18 Scandentia        0.0025  
## 19 Soricomorpha      0.000592
```


```r
msleep %>% 
  filter(order=="Cetacea") %>% 
  select(order, genus, brainwt)
```

```
## # A tibble: 3 × 3
##   order   genus         brainwt
##   <chr>   <chr>           <dbl>
## 1 Cetacea Globicephalus      NA
## 2 Cetacea Phocoena           NA
## 3 Cetacea Tursiops           NA
```

**As biologists, a good question that we may ask is how do the measured variables differ by island on average (on which island has the greatest body weight)**

```r
penguins %>% 
  group_by(island) %>% 
  summarize(mean_mass=mean(body_mass_g),
            mean_bill=mean(bill_length_mm),
            total=n())
```

```
## # A tibble: 3 × 4
##   island    mean_mass mean_bill total
##   <fct>         <dbl>     <dbl> <int>
## 1 Biscoe          NA       NA     168
## 2 Dream         3713.      44.2   124
## 3 Torgersen       NA       NA      52
```


```r
penguins %>% 
  filter(!is.na(body_mass_g)) %>% #pull out all observations with a number (no NA)
  group_by(island) %>% 
  summarize(mean_mass=mean(body_mass_g),
            mean_bill=mean(bill_length_mm),
            total=n())
```

```
## # A tibble: 3 × 4
##   island    mean_mass mean_bill total
##   <fct>         <dbl>     <dbl> <int>
## 1 Biscoe        4716.      45.3   167
## 2 Dream         3713.      44.2   124
## 3 Torgersen     3706.      39.0    51
```

**Interested in the number of observations (penguins) by species and island**

```r
penguins %>% 
  group_by(species, island) %>% 
  summarize(n=n(), .groups= 'keep') #the .groups argument here just prevents a warning message
```

```
## # A tibble: 5 × 3
## # Groups:   species, island [5]
##   species   island        n
##   <fct>     <fct>     <int>
## 1 Adelie    Biscoe       44
## 2 Adelie    Dream        56
## 3 Adelie    Torgersen    52
## 4 Chinstrap Dream        68
## 5 Gentoo    Biscoe      124
```

### count
**`count()` is an easy way of determining how many observations you have within a column. It acts like a combination of `group_by()` and `n()`**

```r
penguins %>% 
  count(island, sort = T) #sort=T sorts the column in descending order
```

```
## # A tibble: 3 × 2
##   island        n
##   <fct>     <int>
## 1 Biscoe      168
## 2 Dream       124
## 3 Torgersen    52
```

**Compare this with `summarize()` and `group_by()`**

```r
penguins %>% 
  group_by(island) %>% 
  summarize(n=n()) 
```

```
## # A tibble: 3 × 2
##   island        n
##   <fct>     <int>
## 1 Biscoe      168
## 2 Dream       124
## 3 Torgersen    52
```

**Use `count()` across multiple variables (can also use tabyl**

```r
penguins %>% 
  count(island, species, sort = T) # sort=T will arrange in descending order
```

```
## # A tibble: 5 × 3
##   island    species       n
##   <fct>     <fct>     <int>
## 1 Biscoe    Gentoo      124
## 2 Dream     Chinstrap    68
## 3 Dream     Adelie       56
## 4 Torgersen Adelie       52
## 5 Biscoe    Adelie       44
```


**Example**
1. How does the mean of `bill_length_mm` compare between penguin species?

```r
penguins %>% 
  group_by(species) %>% 
  summarize(mean_bill=mean(bill_length_mm, na.rm = T))
```

```
## # A tibble: 3 × 2
##   species   mean_bill
##   <fct>         <dbl>
## 1 Adelie         38.8
## 2 Chinstrap      48.8
## 3 Gentoo         47.5
```

2. For some penguins, their sex is listed as NA. Where do these penguins occur?

```r
penguins %>% 
  count(sex, island)
```

```
## # A tibble: 9 × 3
##   sex    island        n
##   <fct>  <fct>     <int>
## 1 female Biscoe       80
## 2 female Dream        61
## 3 female Torgersen    24
## 4 male   Biscoe       83
## 5 male   Dream        62
## 6 male   Torgersen    23
## 7 <NA>   Biscoe        5
## 8 <NA>   Dream         1
## 9 <NA>   Torgersen     5
```


```r
penguins %>% 
  group_by(sex) %>%
  summarize(number_NA=sum(is.na(sex)))
```

```
## # A tibble: 3 × 2
##   sex    number_NA
##   <fct>      <int>
## 1 female         0
## 2 male           0
## 3 <NA>          11
```

### across
**There is a function in dplyr called `across()` which is designed to work across multiple variables** 

**What if we wanted to apply `summarize()` in order to produce distinct counts over multiple variables; i.e. species, island, and sex? Although this isn't a lot of coding you can image that with a lot of variables it would be cumbersome**

```r
penguins %>%
  summarize(distinct_species = n_distinct(species),
            distinct_island = n_distinct(island),
            distinct_sex = n_distinct(sex))
```

```
## # A tibble: 1 × 3
##   distinct_species distinct_island distinct_sex
##              <int>           <int>        <int>
## 1                3               3            3
```

**By using `across()` we can reduce the clutter and make things cleaner**

```r
penguins %>%
  summarize(across(c(species, island, sex), n_distinct)) #summarize across species, island, and sex
```

```
## # A tibble: 1 × 3
##   species island   sex
##     <int>  <int> <int>
## 1       3      3     3
```

**This is very helpful for continuous variables**

```r
penguins %>%
  summarize(across(contains("mm"), mean, na.rm=T))
```

```
## Warning: There was 1 warning in `summarize()`.
## ℹ In argument: `across(contains("mm"), mean, na.rm = T)`.
## Caused by warning:
## ! The `...` argument of `across()` is deprecated as of dplyr 1.1.0.
## Supply arguments directly to `.fns` through an anonymous function instead.
## 
##   # Previously
##   across(a:b, mean, na.rm = TRUE)
## 
##   # Now
##   across(a:b, \(x) mean(x, na.rm = TRUE))
```

```
## # A tibble: 1 × 3
##   bill_length_mm bill_depth_mm flipper_length_mm
##            <dbl>         <dbl>             <dbl>
## 1           43.9          17.2              201.
```


```r
penguins %>%
  summarize(across(contains("mm"), \(x) mean(x, na.rm = TRUE))) #use this to correct the error
```

```
## # A tibble: 1 × 3
##   bill_length_mm bill_depth_mm flipper_length_mm
##            <dbl>         <dbl>             <dbl>
## 1           43.9          17.2              201.
```

**`group_by` also works**

```r
penguins %>%
  group_by(sex) %>% 
  summarize(across(contains("mm"), mean, na.rm=T))
```

```
## # A tibble: 3 × 4
##   sex    bill_length_mm bill_depth_mm flipper_length_mm
##   <fct>           <dbl>         <dbl>             <dbl>
## 1 female           42.1          16.4              197.
## 2 male             45.9          17.9              205.
## 3 <NA>             41.3          16.6              199
```

**Here we summarize across all variables**

```r
penguins %>%
  summarise_all(mean, na.rm=T)
```

```
## Warning: There were 3 warnings in `summarise()`.
## The first warning was:
## ℹ In argument: `species = (function (x, ...) ...`.
## Caused by warning in `mean.default()`:
## ! argument is not numeric or logical: returning NA
## ℹ Run `dplyr::last_dplyr_warnings()` to see the 2 remaining warnings.
```

```
## # A tibble: 1 × 8
##   species island bill_length_mm bill_depth_mm flipper_length_mm body_mass_g
##     <dbl>  <dbl>          <dbl>         <dbl>             <dbl>       <dbl>
## 1      NA     NA           43.9          17.2              201.       4202.
## # ℹ 2 more variables: sex <dbl>, year <dbl>
```

**Operators can also work, here I am summarizing across all variables except `species`, `island`, `sex`, and `year`**

```r
penguins %>%
  summarise(across(!c(species, island, sex, year), 
                   mean, na.rm=T))
```

```
## # A tibble: 1 × 4
##   bill_length_mm bill_depth_mm flipper_length_mm body_mass_g
##            <dbl>         <dbl>             <dbl>       <dbl>
## 1           43.9          17.2              201.       4202.
```

**All variables that include "bill"...all of the other dplyr operators also work**

```r
penguins %>%
  summarise(across(starts_with("bill"), mean, na.rm=T))
```

```
## # A tibble: 1 × 2
##   bill_length_mm bill_depth_mm
##            <dbl>         <dbl>
## 1           43.9          17.2
```

