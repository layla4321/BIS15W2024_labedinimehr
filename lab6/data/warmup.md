---
output: 
  html_document: 
    keep_md: yes
---


## Warm-up
1. Load the `bison.csv` data.

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

```
## # A tibble: 8,325 × 8
##    data_code rec_year rec_month rec_day animal_code animal_sex animal_weight
##    <chr>        <dbl>     <dbl>   <dbl> <chr>       <chr>              <dbl>
##  1 CBH01         1994        11       8 813         F                    890
##  2 CBH01         1994        11       8 834         F                   1074
##  3 CBH01         1994        11       8 B-301       F                   1060
##  4 CBH01         1994        11       8 B-402       F                    989
##  5 CBH01         1994        11       8 B-403       F                   1062
##  6 CBH01         1994        11       8 B-502       F                    978
##  7 CBH01         1994        11       8 B-503       F                   1068
##  8 CBH01         1994        11       8 B-504       F                   1024
##  9 CBH01         1994        11       8 B-601       F                    978
## 10 CBH01         1994        11       8 B-602       F                   1188
## # ℹ 8,315 more rows
## # ℹ 1 more variable: animal_yob <dbl>
```

```
## [1] "/Users/labedini/Desktop/BIS15W2024_labedinimehr/lab6/data"
```

## hav a look
2. What are the dimesions and structure of the data?

```
## Rows: 8,325
## Columns: 8
## $ data_code     <chr> "CBH01", "CBH01", "CBH01", "CBH01", "CBH01", "CBH01", "C…
## $ rec_year      <dbl> 1994, 1994, 1994, 1994, 1994, 1994, 1994, 1994, 1994, 19…
## $ rec_month     <dbl> 11, 11, 11, 11, 11, 11, 11, 11, 11, 11, 11, 11, 11, 11, …
## $ rec_day       <dbl> 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8,…
## $ animal_code   <chr> "813", "834", "B-301", "B-402", "B-403", "B-502", "B-503…
## $ animal_sex    <chr> "F", "F", "F", "F", "F", "F", "F", "F", "F", "F", "F", "…
## $ animal_weight <dbl> 890, 1074, 1060, 989, 1062, 978, 1068, 1024, 978, 1188, …
## $ animal_yob    <dbl> 1981, 1983, 1983, 1984, 1984, 1985, 1985, 1985, 1986, 19…
```

```
## [1] 8325    8
```

3. We are only interested in code, sex, weight, year of birth. Restrict the data to these variables and store the dataframe as a new object.


4. Pull out the animals born between 1980-1990.

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

5. How many male and female bison are represented between 1980-1990?

```
## # A tibble: 21 × 4
##    data_code animal_sex animal_weight animal_yob
##    <chr>     <chr>              <dbl>      <dbl>
##  1 CBH01     M                   1728       1987
##  2 CBH01     M                   1726       1988
##  3 CBH01     M                   1712       1988
##  4 CBH01     M                   1306       1989
##  5 CBH01     M                   1682       1989
##  6 CBH01     M                   1594       1989
##  7 CBH01     M                   1552       1990
##  8 CBH01     M                   1572       1990
##  9 CBH01     M                   1538       1990
## 10 CBH01     M                   1422       1990
## # ℹ 11 more rows
```

```
## 
##  M 
## 21
```


```
## # A tibble: 414 × 4
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
## # ℹ 404 more rows
```

6. Between 1980-1990, were males or females larger on average?

```
## [1] 1543.333
```

```
## [1] 1017.314
```

