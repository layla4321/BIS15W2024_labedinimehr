---
output: 
  html_document: 
    keep_md: yes
---
           ---
title: "Transforming data 1: Dplyr `select()`"
date: "2024-01-23"
output:
  html_document:
    theme: spacelab
    toc: yes
    toc_float: yes
  pdf_document:
    toc: yes
---

## Learning Goals
*At the end of this exercise, you will be able to:*    
1. Use summary functions to assess the structure of a data frame.  
2. Us the select function of `dplyr` to build data frames restricted to variable of interest.  
3. Use the `rename()` function to provide new, consistent names to variables in data frames.  

## Load the tidyverse
For the remainder of the quarter, we will work within the `tidyverse`. At the start of each lab, the library needs to be loaded as shown below.  

```r
library("tidyverse")
```

## Load the data
These data are from: Gaeta J., G. Sass, S. Carpenter. 2012. Biocomplexity at North Temperate Lakes LTER: Coordinated Field Studies: Large Mouth Bass Growth 2006. Environmental Data Initiative.  [link](https://portal.edirepository.org/nis/mapbrowse?scope=knb-lter-ntl&identifier=267)  

```r
fish <- readr::read_csv("data/Gaeta_etal_CLC_data.csv")
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

## Data Structure
Once data have been uploaded, let's get an idea of its structure, contents, and dimensions.  

```r
glimpse(fish)
```

```
## Rows: 4,033
## Columns: 6
## $ lakeid          <chr> "AL", "AL", "AL", "AL", "AL", "AL", "AL", "AL", "AL", …
## $ fish_id         <dbl> 299, 299, 299, 300, 300, 300, 300, 301, 301, 301, 301,…
## $ annnumber       <chr> "EDGE", "2", "1", "EDGE", "3", "2", "1", "EDGE", "3", …
## $ length          <dbl> 167, 167, 167, 175, 175, 175, 175, 194, 194, 194, 194,…
## $ radii_length_mm <dbl> 2.697443, 2.037518, 1.311795, 3.015477, 2.670733, 2.13…
## $ scalelength     <dbl> 2.697443, 2.697443, 2.697443, 3.015477, 3.015477, 3.01…
```

```r
dim(fish)
```

```
## [1] 4033    6
```

```r
summary(fish)
```

```
##     lakeid             fish_id       annnumber             length     
##  Length:4033        Min.   :  1.0   Length:4033        Min.   : 58.0  
##  Class :character   1st Qu.:156.0   Class :character   1st Qu.:253.0  
##  Mode  :character   Median :267.0   Mode  :character   Median :299.0  
##                     Mean   :258.3                      Mean   :293.3  
##                     3rd Qu.:376.0                      3rd Qu.:342.0  
##                     Max.   :478.0                      Max.   :420.0  
##  radii_length_mm    scalelength     
##  Min.   : 0.4569   Min.   : 0.6282  
##  1st Qu.: 2.3252   1st Qu.: 4.2596  
##  Median : 3.5380   Median : 5.4062  
##  Mean   : 3.6589   Mean   : 5.3821  
##  3rd Qu.: 4.8229   3rd Qu.: 6.4145  
##  Max.   :11.0258   Max.   :11.0258
```

## Tidyverse
The [tidyverse](www.tidyverse.org) is an "opinionated" collection of packages that make workflow in R easier. The packages operate more intuitively than base R commands and share a common organizational philosophy.  
![*Data Science Workflow in the Tidyverse.*](tidy-1.png)  

## dplyr
The first package that we will use that is part of the tidyverse is `dplyr`. `dplyr` is used to transform data frames by extracting, rearranging, and summarizing data such that they are focused on a question of interest. This is very helpful,  especially when wrangling large data, and makes dplyr one of most frequently used packages in the tidyverse. The two functions we will use most are `select()` and `filter()`.  

## `select()`
Select allows you to pull out columns of interest from a dataframe. To do this, just add the names of the columns to the `select()` command. The order in which you add them, will determine the order in which they appear in the output.

```r
names(fish)
```

```
## [1] "lakeid"          "fish_id"         "annnumber"       "length"         
## [5] "radii_length_mm" "scalelength"
```

```r
fish_subset <- select(fish, "fish_id", "length")
```


We are only interested in lakeid and scalelength.

```r
select(fish, "lakeid", "scalelength")
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

To add a range of columns use `start_col:end_col`.

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

The - operator is useful in select. It allows us to select everything except the specified variables.

```r
select(fish, -fish_id, -annnumber, -length, -radii_length_mm)
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

For very large data frames with lots of variables, `select()` utilizes lots of different operators to make things easier. Let's say we are only interested in the variables that deal with length.


```r
names(fish)
```

```
## [1] "lakeid"          "fish_id"         "annnumber"       "length"         
## [5] "radii_length_mm" "scalelength"
```


```r
select(fish, contains("length"))
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

When columns are sequentially named, `starts_with()` makes selecting columns easier.

```r
select(fish, starts_with("radii"))
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
select(fish, matches("a.+er")) ##soooo important for proj
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

Options to select columns based on a specific criteria include:  
1. ends_with() = Select columns that end with a character string  
2. contains() = Select columns that contain a character string  
3. matches() = Select columns that match a regular expression  
4. one_of() = Select columns names that are from a group of names  



```r
names(fish)
```

```
## [1] "lakeid"          "fish_id"         "annnumber"       "length"         
## [5] "radii_length_mm" "scalelength"
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
select(fish, contains("fish"))
```

```
## # A tibble: 4,033 × 1
##    fish_id
##      <dbl>
##  1     299
##  2     299
##  3     299
##  4     300
##  5     300
##  6     300
##  7     300
##  8     301
##  9     301
## 10     301
## # ℹ 4,023 more rows
```

We won't cover regular expressions [regex](https://en.wikipedia.org/wiki/Regular_expression) in this class, but the following code is helpful when you know that a column contains a letter (in this case "a") followed by a subsequent string (in this case "er").  

```r
select(fish, matches("a.+er"))
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

You can also select columns based on the class of data.  

```r
glimpse(fish)
```

```
## Rows: 4,033
## Columns: 6
## $ lakeid          <chr> "AL", "AL", "AL", "AL", "AL", "AL", "AL", "AL", "AL", …
## $ fish_id         <dbl> 299, 299, 299, 300, 300, 300, 300, 301, 301, 301, 301,…
## $ annnumber       <chr> "EDGE", "2", "1", "EDGE", "3", "2", "1", "EDGE", "3", …
## $ length          <dbl> 167, 167, 167, 175, 175, 175, 175, 194, 194, 194, 194,…
## $ radii_length_mm <dbl> 2.697443, 2.037518, 1.311795, 3.015477, 2.670733, 2.13…
## $ scalelength     <dbl> 2.697443, 2.697443, 2.697443, 3.015477, 3.015477, 3.01…
```


```r
select_if(fish, is.numeric)
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

To select all columns that are *not* a class of data, you need to add a `~`.

```r
select_if(fish, ~!is.numeric(.)) ##! means not
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

## Practice  
For this exercise we will use life history data `mammal_lifehistories_v2.csv` for mammals. The [data](http://esapubs.org/archive/ecol/E084/093/) are from:  
**S. K. Morgan Ernest. 2003. Life history characteristics of placental non-volant mammals. Ecology 84:3402.**  

Load the data.  

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

1. Use one or more of your favorite functions to assess the structure of the data.  

```r
str(mammals)
```

```
## spc_tbl_ [1,440 × 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ order       : chr [1:1440] "Artiodactyla" "Artiodactyla" "Artiodactyla" "Artiodactyla" ...
##  $ family      : chr [1:1440] "Antilocapridae" "Bovidae" "Bovidae" "Bovidae" ...
##  $ Genus       : chr [1:1440] "Antilocapra" "Addax" "Aepyceros" "Alcelaphus" ...
##  $ species     : chr [1:1440] "americana" "nasomaculatus" "melampus" "buselaphus" ...
##  $ mass        : num [1:1440] 45375 182375 41480 150000 28500 ...
##  $ gestation   : num [1:1440] 8.13 9.39 6.35 7.9 6.8 5.08 5.72 5.5 8.93 9.14 ...
##  $ newborn     : num [1:1440] 3246 5480 5093 10167 -999 ...
##  $ weaning     : num [1:1440] 3 6.5 5.63 6.5 -999 ...
##  $ wean mass   : num [1:1440] 8900 -999 15900 -999 -999 ...
##  $ AFR         : num [1:1440] 13.5 27.3 16.7 23 -999 ...
##  $ max. life   : num [1:1440] 142 308 213 240 -999 251 228 255 300 324 ...
##  $ litter size : num [1:1440] 1.85 1 1 1 1 1.37 1 1 1 1 ...
##  $ litters/year: num [1:1440] 1 0.99 0.95 -999 -999 2 -999 1.89 1 1 ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   order = col_character(),
##   ..   family = col_character(),
##   ..   Genus = col_character(),
##   ..   species = col_character(),
##   ..   mass = col_double(),
##   ..   gestation = col_double(),
##   ..   newborn = col_double(),
##   ..   weaning = col_double(),
##   ..   `wean mass` = col_double(),
##   ..   AFR = col_double(),
##   ..   `max. life` = col_double(),
##   ..   `litter size` = col_double(),
##   ..   `litters/year` = col_double()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

2. Are there any NAs? Are you sure? Try taking an average of `max. life` as a test.  

```r
anyNA(mammals)
```

```
## [1] FALSE
```

```r
summary(mammals)
```

```
##     order              family             Genus             species         
##  Length:1440        Length:1440        Length:1440        Length:1440       
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##       mass             gestation          newborn             weaning       
##  Min.   :     -999   Min.   :-999.00   Min.   :   -999.0   Min.   :-999.00  
##  1st Qu.:       50   1st Qu.:-999.00   1st Qu.:   -999.0   1st Qu.:-999.00  
##  Median :      403   Median :   1.05   Median :      2.6   Median :   0.73  
##  Mean   :   383577   Mean   :-287.25   Mean   :   6703.1   Mean   :-427.17  
##  3rd Qu.:     7009   3rd Qu.:   4.50   3rd Qu.:     98.0   3rd Qu.:   2.00  
##  Max.   :149000000   Max.   :  21.46   Max.   :2250000.0   Max.   :  48.00  
##    wean mass             AFR            max. life       litter size      
##  Min.   :    -999   Min.   :-999.00   Min.   :-999.0   Min.   :-999.000  
##  1st Qu.:    -999   1st Qu.:-999.00   1st Qu.:-999.0   1st Qu.:   1.000  
##  Median :    -999   Median :   2.50   Median :-999.0   Median :   2.270  
##  Mean   :   16049   Mean   :-408.12   Mean   :-490.3   Mean   : -55.634  
##  3rd Qu.:      10   3rd Qu.:  15.61   3rd Qu.: 147.2   3rd Qu.:   3.835  
##  Max.   :19075000   Max.   : 210.00   Max.   :1368.0   Max.   :  14.180  
##   litters/year     
##  Min.   :-999.000  
##  1st Qu.:-999.000  
##  Median :   0.375  
##  Mean   :-477.141  
##  3rd Qu.:   1.155  
##  Max.   :   7.500
```

```r
mean(mammals$`max. life`)
```

```
## [1] -490.2556
```

3. What are the names of the columns in the `mammals` data?

```r
names(mammals)
```

```
##  [1] "order"        "family"       "Genus"        "species"      "mass"        
##  [6] "gestation"    "newborn"      "weaning"      "wean mass"    "AFR"         
## [11] "max. life"    "litter size"  "litters/year"
```

4. Rename any columns that have capitol letters or punctuation issues.  

```r
mammals_new <- rename(mammals, afr="AFR", genus="Genus", litters_year="litters/year", max_life="max. life", litter_size="litter size", wean_mass="wean mass")
```

5. We are only interested in the variables `genus`, `species`, and `mass`. Use `select()` to build a new dataframe `mass` focused on these variables.

```r
mass <- select(mammals_new, "genus", "species", "mass")
mass
```

```
## # A tibble: 1,440 × 3
##    genus       species          mass
##    <chr>       <chr>           <dbl>
##  1 Antilocapra americana      45375 
##  2 Addax       nasomaculatus 182375 
##  3 Aepyceros   melampus       41480 
##  4 Alcelaphus  buselaphus    150000 
##  5 Ammodorcas  clarkei        28500 
##  6 Ammotragus  lervia         55500 
##  7 Antidorcas  marsupialis    30000 
##  8 Antilope    cervicapra     37500 
##  9 Bison       bison         497667.
## 10 Bison       bonasus       500000 
## # ℹ 1,430 more rows
```

6. What if we only wanted to exclude `order` and `family`? Use the `-` operator to make the code efficient.

```r
select(mammals_new, -"order", -"family")
```

```
## # A tibble: 1,440 × 11
##    genus      species   mass gestation newborn weaning wean_mass    afr max_life
##    <chr>      <chr>    <dbl>     <dbl>   <dbl>   <dbl>     <dbl>  <dbl>    <dbl>
##  1 Antilocap… americ… 4.54e4      8.13   3246.    3         8900   13.5      142
##  2 Addax      nasoma… 1.82e5      9.39   5480     6.5       -999   27.3      308
##  3 Aepyceros  melamp… 4.15e4      6.35   5093     5.63     15900   16.7      213
##  4 Alcelaphus busela… 1.5 e5      7.9   10167.    6.5       -999   23.0      240
##  5 Ammodorcas clarkei 2.85e4      6.8    -999  -999         -999 -999       -999
##  6 Ammotragus lervia  5.55e4      5.08   3810     4         -999   14.9      251
##  7 Antidorcas marsup… 3   e4      5.72   3910     4.04      -999   10.2      228
##  8 Antilope   cervic… 3.75e4      5.5    3846     2.13      -999   20.1      255
##  9 Bison      bison   4.98e5      8.93  20000    10.7     157500   29.4      300
## 10 Bison      bonasus 5   e5      9.14  23000.    6.6       -999   30.0      324
## # ℹ 1,430 more rows
## # ℹ 2 more variables: litter_size <dbl>, litters_year <dbl>
```

7. Select the columns that include "mass" as part of the name.  

```r
select(mammals_new, contains("mass"))
```

```
## # A tibble: 1,440 × 2
##       mass wean_mass
##      <dbl>     <dbl>
##  1  45375       8900
##  2 182375       -999
##  3  41480      15900
##  4 150000       -999
##  5  28500       -999
##  6  55500       -999
##  7  30000       -999
##  8  37500       -999
##  9 497667.    157500
## 10 500000       -999
## # ℹ 1,430 more rows
```

8. Select all of the columns that are of class `character`.  

```r
select_if(mammals_new, ~is.character(.))
```

```
## # A tibble: 1,440 × 4
##    order        family         genus       species      
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

## Other
Here are two examples of code that are super helpful to have in your bag of tricks.  

Imported data frames often have a mix of lower and uppercase column names. Use `toupper()` or `tolower()` to fix this issue. I always try to use lowercase to keep things consistent.  

```r
mammals <- select_all(mammals,toupper)
```


```r
library(janitor)
```

```
## 
## Attaching package: 'janitor'
```

```
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```

```r
names(mammals)
```

```
##  [1] "ORDER"        "FAMILY"       "GENUS"        "SPECIES"      "MASS"        
##  [6] "GESTATION"    "NEWBORN"      "WEANING"      "WEAN MASS"    "AFR"         
## [11] "MAX. LIFE"    "LITTER SIZE"  "LITTERS/YEAR"
```

```r
clean_names(mammals)
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

When naming columns, blank spaces are often added (don't do this, please). Here is a trick to remove these.  

```r
#select_all(mammals, ~str_replace(., " ", "_"))
```

## That's it! Let's take a break and then move on to part 2! 

-->[Home](https://jmledford3115.github.io/datascibiol/)  
