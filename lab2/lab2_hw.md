---
title: "Lab 2 Homework"
author: Layla Abedinimehr
date: "2024-01-17"
output:
  html_document: 
    theme: spacelab
    keep_md: true
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

1. What is a vector in R?  
A vector helps you organize data. You use C (concatenate) to create and organize the vectors. 

2. What is a data matrix in R?  
They are vectors organized into lists and columns that look like a data table. 

3. Below are data collected by three scientists (Jill, Steve, Susan in order) measuring temperatures of eight hot springs. Run this code chunk to create the vectors.  

```r
spring_1 <- c(36.25, 35.40, 35.30)
spring_2 <- c(35.15, 35.35, 33.35)
spring_3 <- c(30.70, 29.65, 29.20)
spring_4 <- c(39.70, 40.05, 38.65)
spring_5 <- c(31.85, 31.40, 29.30)
spring_6 <- c(30.20, 30.65, 29.75)
spring_7 <- c(32.90, 32.50, 32.80)
spring_8 <- c(36.80, 36.45, 33.15)
```

4. Build a data matrix that has the springs as rows and the columns as scientists.  

```r
scientists <- c("jill", "steve", "susan")
```


```r
springs <- c(spring_1, spring_2, spring_3, spring_4, spring_5, spring_6, spring_7, spring_8)
```


```r
reasearch_matrix <- matrix(springs, nrow = 8, byrow = 3 )
```


```r
reasearch_matrix
```

```
##       [,1]  [,2]  [,3]
## [1,] 36.25 35.40 35.30
## [2,] 35.15 35.35 33.35
## [3,] 30.70 29.65 29.20
## [4,] 39.70 40.05 38.65
## [5,] 31.85 31.40 29.30
## [6,] 30.20 30.65 29.75
## [7,] 32.90 32.50 32.80
## [8,] 36.80 36.45 33.15
```



5. The names of the springs are 1.Bluebell Spring, 2.Opal Spring, 3.Riverside Spring, 4.Too Hot Spring, 5.Mystery Spring, 6.Emerald Spring, 7.Black Spring, 8.Pearl Spring. Name the rows and columns in the data matrix. Start by making two new vectors with the names, then use `colnames()` and `rownames()` to name the columns and rows.

```r
springnames <- c("Bluebell Spring", "Opal Spring", "Riverside Spring", "Too Hot Spring", "Mystery Spring", "Emerald Spring", "Black Spring", "Pearl Spring")
```


```r
springnames
```

```
## [1] "Bluebell Spring"  "Opal Spring"      "Riverside Spring" "Too Hot Spring"  
## [5] "Mystery Spring"   "Emerald Spring"   "Black Spring"     "Pearl Spring"
```

```r
studiedby <- c("jill", "steve", "susan")
```


```r
studiedby
```

```
## [1] "jill"  "steve" "susan"
```

```r
rownames(reasearch_matrix) <- springnames
```

```r
colnames(reasearch_matrix) <- studiedby
```

```r
reasearch_matrix
```

```
##                   jill steve susan
## Bluebell Spring  36.25 35.40 35.30
## Opal Spring      35.15 35.35 33.35
## Riverside Spring 30.70 29.65 29.20
## Too Hot Spring   39.70 40.05 38.65
## Mystery Spring   31.85 31.40 29.30
## Emerald Spring   30.20 30.65 29.75
## Black Spring     32.90 32.50 32.80
## Pearl Spring     36.80 36.45 33.15
```


6. Calculate the mean temperature of all eight springs.

```r
mean(springs)
```

```
## [1] 33.60417
```


7. Add this as a new column in the data matrix.  

```r
cbind(mean(springs))
```

```
##          [,1]
## [1,] 33.60417
```


```r
Mean <- mean(reasearch_matrix)
```


```r
Mean
```

```
## [1] 33.60417
```


```r
reasearch_matrix <- cbind(reasearch_matrix, Mean)
```


```r
reasearch_matrix
```

```
##                   jill steve susan     Mean
## Bluebell Spring  36.25 35.40 35.30 33.60417
## Opal Spring      35.15 35.35 33.35 33.60417
## Riverside Spring 30.70 29.65 29.20 33.60417
## Too Hot Spring   39.70 40.05 38.65 33.60417
## Mystery Spring   31.85 31.40 29.30 33.60417
## Emerald Spring   30.20 30.65 29.75 33.60417
## Black Spring     32.90 32.50 32.80 33.60417
## Pearl Spring     36.80 36.45 33.15 33.60417
```


8. Show Susan's value for Opal Spring only.

```r
reasearch_matrix[2,3]
```

```
## [1] 33.35
```

```r
reasearch_matrix["Opal Spring", "susan"]
```

```
## [1] 33.35
```


9. Calculate the mean for Jill's column only.  

```r
mean(reasearch_matrix[,"jill"])
```

```
## [1] 34.19375
```


10. Use the data matrix to perform one calculation or operation of your interest.

```r
rowSums(reasearch_matrix)
```

```
##  Bluebell Spring      Opal Spring Riverside Spring   Too Hot Spring 
##         140.5542         137.4542         123.1542         152.0042 
##   Mystery Spring   Emerald Spring     Black Spring     Pearl Spring 
##         126.1542         124.2042         131.8042         140.0042
```


## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.  