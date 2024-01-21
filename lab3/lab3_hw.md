---
title: "Lab 3 Homework"
author: "Layla Abedinimehr"
date: "2024-01-21"
output:
  html_document: 
    theme: spacelab
    keep_md: true
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the tidyverse

```r
library(tidyverse)
```

### Mammals Sleep  
1. For this assignment, we are going to use built-in data on mammal sleep patterns. From which publication are these data taken from? Since the data are built-in you can use the help function in R. The name of the data is `msleep`.  

```r
msleep <- msleep
```

2. Store these data into a new data frame `sleep`.  

```r
sleep <- data.frame("msleep")
```

3. What are the dimensions of this data frame (variables and observations)? How do you know? Please show the *code* that you used to determine this below.  

```r
dim(sleep)
```

```
## [1] 1 1
```

4. Are there any NAs in the data? How did you determine this? Please show your code.  

```r
is.na(sleep)
```

```
##      X.msleep.
## [1,]     FALSE
```

5. Show a list of the column names is this data frame.

```r
names(msleep)
```

```
##  [1] "name"         "genus"        "vore"         "order"        "conservation"
##  [6] "sleep_total"  "sleep_rem"    "sleep_cycle"  "awake"        "brainwt"     
## [11] "bodywt"
```

6. How many herbivores are represented in the data?  

```r
table(msleep$vore)
```

```
## 
##   carni   herbi insecti    omni 
##      19      32       5      20
```

7. We are interested in two groups; small and large mammals. Let's define small as less than or equal to 19kg body weight and large as greater than or equal to 200kg body weight. Make two new dataframes (large and small) based on these parameters.

```r
small_mammal <- filter(msleep, bodywt<=19)
small_mammal
```

```
## # A tibble: 59 × 11
##    name   genus vore  order conservation sleep_total sleep_rem sleep_cycle awake
##    <chr>  <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl> <dbl>
##  1 Owl m… Aotus omni  Prim… <NA>                17         1.8      NA       7  
##  2 Mount… Aplo… herbi Rode… nt                  14.4       2.4      NA       9.6
##  3 Great… Blar… omni  Sori… lc                  14.9       2.3       0.133   9.1
##  4 Three… Brad… herbi Pilo… <NA>                14.4       2.2       0.767   9.6
##  5 Vespe… Calo… <NA>  Rode… <NA>                 7        NA        NA      17  
##  6 Dog    Canis carni Carn… domesticated        10.1       2.9       0.333  13.9
##  7 Roe d… Capr… herbi Arti… lc                   3        NA        NA      21  
##  8 Guine… Cavis herbi Rode… domesticated         9.4       0.8       0.217  14.6
##  9 Grivet Cerc… omni  Prim… lc                  10         0.7      NA      14  
## 10 Chinc… Chin… herbi Rode… domesticated        12.5       1.5       0.117  11.5
## # ℹ 49 more rows
## # ℹ 2 more variables: brainwt <dbl>, bodywt <dbl>
```

```r
large_mammal <- filter(msleep, bodywt>=200)
large_mammal
```

```
## # A tibble: 7 × 11
##   name    genus vore  order conservation sleep_total sleep_rem sleep_cycle awake
##   <chr>   <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl> <dbl>
## 1 Cow     Bos   herbi Arti… domesticated         4         0.7       0.667  20  
## 2 Asian … Elep… herbi Prob… en                   3.9      NA        NA      20.1
## 3 Horse   Equus herbi Peri… domesticated         2.9       0.6       1      21.1
## 4 Giraffe Gira… herbi Arti… cd                   1.9       0.4      NA      22.1
## 5 Pilot … Glob… carni Ceta… cd                   2.7       0.1      NA      21.4
## 6 Africa… Loxo… herbi Prob… vu                   3.3      NA        NA      20.7
## 7 Brazil… Tapi… herbi Peri… vu                   4.4       1         0.9    19.6
## # ℹ 2 more variables: brainwt <dbl>, bodywt <dbl>
```

8. What is the mean weight for both the small and large mammals?

```r
mean(small_mammal$bodywt)
```

```
## [1] 1.797847
```


```r
mean(large_mammal$bodywt)
```

```
## [1] 1747.071
```

9. Using a similar approach as above, do large or small animals sleep longer on average?  


```r
mean(large_mammal$sleep_total)
```

```
## [1] 3.3
```

```r
mean(small_mammal$sleep_total)
```

```
## [1] 11.78644
```
 No the small animals sleep total is longer than the large mammals. 

10. Which animal is the sleepiest among the entire dataframe?

```r
max(msleep$sleep_total)
```

```
## [1] 19.9
```

```r
sleepy_head <- filter(msleep, sleep_total==19.9)
sleepy_head$name
```

```
## [1] "Little brown bat"
```


## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
