---
title: "Lab 7 Homework"
author: "Layla Abedinimehr"
date: "2024-02-05"
output:
  html_document: 
    theme: spacelab
    keep_md: true
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
library(skimr)
```

For this assignment we are going to work with a large data set from the [United Nations Food and Agriculture Organization](http://www.fao.org/about/en/) on world fisheries. These data are pretty wild, so we need to do some cleaning. First, load the data.  

Load the data `FAO_1950to2012_111914.csv` as a new object titled `fisheries`.

```r
fisheries <- readr::read_csv(file = "data/FAO_1950to2012_111914.csv")
```

```
## Rows: 17692 Columns: 71
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (69): Country, Common name, ISSCAAP taxonomic group, ASFIS species#, ASF...
## dbl  (2): ISSCAAP group#, FAO major fishing area
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

1. Do an exploratory analysis of the data (your choice). What are the names of the variables, what are the dimensions, are there any NA's, what are the classes of the variables?  

```r
dim(fisheries)
```

```
## [1] 17692    71
```

```r
head(fisheries)
```

```
## # A tibble: 6 × 71
##   Country `Common name` `ISSCAAP group#` ISSCAAP taxonomic gr…¹ `ASFIS species#`
##   <chr>   <chr>                    <dbl> <chr>                  <chr>           
## 1 Albania Angelsharks,…               38 Sharks, rays, chimaer… 10903XXXXX      
## 2 Albania Atlantic bon…               36 Tunas, bonitos, billf… 1750100101      
## 3 Albania Barracudas n…               37 Miscellaneous pelagic… 17710001XX      
## 4 Albania Blue and red…               45 Shrimps, prawns        2280203101      
## 5 Albania Blue whiting…               32 Cods, hakes, haddocks  1480403301      
## 6 Albania Bluefish                    37 Miscellaneous pelagic… 1702021301      
## # ℹ abbreviated name: ¹​`ISSCAAP taxonomic group`
## # ℹ 66 more variables: `ASFIS species name` <chr>,
## #   `FAO major fishing area` <dbl>, Measure <chr>, `1950` <chr>, `1951` <chr>,
## #   `1952` <chr>, `1953` <chr>, `1954` <chr>, `1955` <chr>, `1956` <chr>,
## #   `1957` <chr>, `1958` <chr>, `1959` <chr>, `1960` <chr>, `1961` <chr>,
## #   `1962` <chr>, `1963` <chr>, `1964` <chr>, `1965` <chr>, `1966` <chr>,
## #   `1967` <chr>, `1968` <chr>, `1969` <chr>, `1970` <chr>, `1971` <chr>, …
```


```r
tail(fisheries)
```

```
## # A tibble: 6 × 71
##   Country `Common name` `ISSCAAP group#` ISSCAAP taxonomic gr…¹ `ASFIS species#`
##   <chr>   <chr>                    <dbl> <chr>                  <chr>           
## 1 Zanzib… Seerfishes n…               36 Tunas, bonitos, billf… 17501015XX      
## 2 Zanzib… Sharks, rays…               38 Sharks, rays, chimaer… 199XXXXXXX054   
## 3 Zanzib… Snappers, jo…               33 Miscellaneous coastal… 17032XXXXX      
## 4 Zanzib… Spinefeet(=R…               33 Miscellaneous coastal… 17407001XX      
## 5 Zanzib… Tropical spi…               43 Lobsters, spinyrock l… 22901001XX      
## 6 Zanzib… Tunalike fis…               36 Tunas, bonitos, billf… 175XXXXXXX      
## # ℹ abbreviated name: ¹​`ISSCAAP taxonomic group`
## # ℹ 66 more variables: `ASFIS species name` <chr>,
## #   `FAO major fishing area` <dbl>, Measure <chr>, `1950` <chr>, `1951` <chr>,
## #   `1952` <chr>, `1953` <chr>, `1954` <chr>, `1955` <chr>, `1956` <chr>,
## #   `1957` <chr>, `1958` <chr>, `1959` <chr>, `1960` <chr>, `1961` <chr>,
## #   `1962` <chr>, `1963` <chr>, `1964` <chr>, `1965` <chr>, `1966` <chr>,
## #   `1967` <chr>, `1968` <chr>, `1969` <chr>, `1970` <chr>, `1971` <chr>, …
```


```r
str(fisheries)
```

```
## spc_tbl_ [17,692 × 71] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ Country                : chr [1:17692] "Albania" "Albania" "Albania" "Albania" ...
##  $ Common name            : chr [1:17692] "Angelsharks, sand devils nei" "Atlantic bonito" "Barracudas nei" "Blue and red shrimp" ...
##  $ ISSCAAP group#         : num [1:17692] 38 36 37 45 32 37 33 45 38 57 ...
##  $ ISSCAAP taxonomic group: chr [1:17692] "Sharks, rays, chimaeras" "Tunas, bonitos, billfishes" "Miscellaneous pelagic fishes" "Shrimps, prawns" ...
##  $ ASFIS species#         : chr [1:17692] "10903XXXXX" "1750100101" "17710001XX" "2280203101" ...
##  $ ASFIS species name     : chr [1:17692] "Squatinidae" "Sarda sarda" "Sphyraena spp" "Aristeus antennatus" ...
##  $ FAO major fishing area : num [1:17692] 37 37 37 37 37 37 37 37 37 37 ...
##  $ Measure                : chr [1:17692] "Quantity (tonnes)" "Quantity (tonnes)" "Quantity (tonnes)" "Quantity (tonnes)" ...
##  $ 1950                   : chr [1:17692] NA NA NA NA ...
##  $ 1951                   : chr [1:17692] NA NA NA NA ...
##  $ 1952                   : chr [1:17692] NA NA NA NA ...
##  $ 1953                   : chr [1:17692] NA NA NA NA ...
##  $ 1954                   : chr [1:17692] NA NA NA NA ...
##  $ 1955                   : chr [1:17692] NA NA NA NA ...
##  $ 1956                   : chr [1:17692] NA NA NA NA ...
##  $ 1957                   : chr [1:17692] NA NA NA NA ...
##  $ 1958                   : chr [1:17692] NA NA NA NA ...
##  $ 1959                   : chr [1:17692] NA NA NA NA ...
##  $ 1960                   : chr [1:17692] NA NA NA NA ...
##  $ 1961                   : chr [1:17692] NA NA NA NA ...
##  $ 1962                   : chr [1:17692] NA NA NA NA ...
##  $ 1963                   : chr [1:17692] NA NA NA NA ...
##  $ 1964                   : chr [1:17692] NA NA NA NA ...
##  $ 1965                   : chr [1:17692] NA NA NA NA ...
##  $ 1966                   : chr [1:17692] NA NA NA NA ...
##  $ 1967                   : chr [1:17692] NA NA NA NA ...
##  $ 1968                   : chr [1:17692] NA NA NA NA ...
##  $ 1969                   : chr [1:17692] NA NA NA NA ...
##  $ 1970                   : chr [1:17692] NA NA NA NA ...
##  $ 1971                   : chr [1:17692] NA NA NA NA ...
##  $ 1972                   : chr [1:17692] NA NA NA NA ...
##  $ 1973                   : chr [1:17692] NA NA NA NA ...
##  $ 1974                   : chr [1:17692] NA NA NA NA ...
##  $ 1975                   : chr [1:17692] NA NA NA NA ...
##  $ 1976                   : chr [1:17692] NA NA NA NA ...
##  $ 1977                   : chr [1:17692] NA NA NA NA ...
##  $ 1978                   : chr [1:17692] NA NA NA NA ...
##  $ 1979                   : chr [1:17692] NA NA NA NA ...
##  $ 1980                   : chr [1:17692] NA NA NA NA ...
##  $ 1981                   : chr [1:17692] NA NA NA NA ...
##  $ 1982                   : chr [1:17692] NA NA NA NA ...
##  $ 1983                   : chr [1:17692] NA NA NA NA ...
##  $ 1984                   : chr [1:17692] NA NA NA NA ...
##  $ 1985                   : chr [1:17692] NA NA NA NA ...
##  $ 1986                   : chr [1:17692] NA NA NA NA ...
##  $ 1987                   : chr [1:17692] NA NA NA NA ...
##  $ 1988                   : chr [1:17692] NA NA NA NA ...
##  $ 1989                   : chr [1:17692] NA NA NA NA ...
##  $ 1990                   : chr [1:17692] NA NA NA NA ...
##  $ 1991                   : chr [1:17692] NA NA NA NA ...
##  $ 1992                   : chr [1:17692] NA NA NA NA ...
##  $ 1993                   : chr [1:17692] NA NA NA NA ...
##  $ 1994                   : chr [1:17692] NA NA NA NA ...
##  $ 1995                   : chr [1:17692] "0 0" "1" NA "0 0" ...
##  $ 1996                   : chr [1:17692] "53" "2" NA "3" ...
##  $ 1997                   : chr [1:17692] "20" "0 0" NA "0 0" ...
##  $ 1998                   : chr [1:17692] "31" "12" NA NA ...
##  $ 1999                   : chr [1:17692] "30" "30" NA NA ...
##  $ 2000                   : chr [1:17692] "30" "25" "2" NA ...
##  $ 2001                   : chr [1:17692] "16" "30" NA NA ...
##  $ 2002                   : chr [1:17692] "79" "24" NA "34" ...
##  $ 2003                   : chr [1:17692] "1" "4" NA "22" ...
##  $ 2004                   : chr [1:17692] "4" "2" "2" "15" ...
##  $ 2005                   : chr [1:17692] "68" "23" "4" "12" ...
##  $ 2006                   : chr [1:17692] "55" "30" "7" "18" ...
##  $ 2007                   : chr [1:17692] "12" "19" NA NA ...
##  $ 2008                   : chr [1:17692] "23" "27" NA NA ...
##  $ 2009                   : chr [1:17692] "14" "21" NA NA ...
##  $ 2010                   : chr [1:17692] "78" "23" "7" NA ...
##  $ 2011                   : chr [1:17692] "12" "12" NA NA ...
##  $ 2012                   : chr [1:17692] "5" "5" NA NA ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   Country = col_character(),
##   ..   `Common name` = col_character(),
##   ..   `ISSCAAP group#` = col_double(),
##   ..   `ISSCAAP taxonomic group` = col_character(),
##   ..   `ASFIS species#` = col_character(),
##   ..   `ASFIS species name` = col_character(),
##   ..   `FAO major fishing area` = col_double(),
##   ..   Measure = col_character(),
##   ..   `1950` = col_character(),
##   ..   `1951` = col_character(),
##   ..   `1952` = col_character(),
##   ..   `1953` = col_character(),
##   ..   `1954` = col_character(),
##   ..   `1955` = col_character(),
##   ..   `1956` = col_character(),
##   ..   `1957` = col_character(),
##   ..   `1958` = col_character(),
##   ..   `1959` = col_character(),
##   ..   `1960` = col_character(),
##   ..   `1961` = col_character(),
##   ..   `1962` = col_character(),
##   ..   `1963` = col_character(),
##   ..   `1964` = col_character(),
##   ..   `1965` = col_character(),
##   ..   `1966` = col_character(),
##   ..   `1967` = col_character(),
##   ..   `1968` = col_character(),
##   ..   `1969` = col_character(),
##   ..   `1970` = col_character(),
##   ..   `1971` = col_character(),
##   ..   `1972` = col_character(),
##   ..   `1973` = col_character(),
##   ..   `1974` = col_character(),
##   ..   `1975` = col_character(),
##   ..   `1976` = col_character(),
##   ..   `1977` = col_character(),
##   ..   `1978` = col_character(),
##   ..   `1979` = col_character(),
##   ..   `1980` = col_character(),
##   ..   `1981` = col_character(),
##   ..   `1982` = col_character(),
##   ..   `1983` = col_character(),
##   ..   `1984` = col_character(),
##   ..   `1985` = col_character(),
##   ..   `1986` = col_character(),
##   ..   `1987` = col_character(),
##   ..   `1988` = col_character(),
##   ..   `1989` = col_character(),
##   ..   `1990` = col_character(),
##   ..   `1991` = col_character(),
##   ..   `1992` = col_character(),
##   ..   `1993` = col_character(),
##   ..   `1994` = col_character(),
##   ..   `1995` = col_character(),
##   ..   `1996` = col_character(),
##   ..   `1997` = col_character(),
##   ..   `1998` = col_character(),
##   ..   `1999` = col_character(),
##   ..   `2000` = col_character(),
##   ..   `2001` = col_character(),
##   ..   `2002` = col_character(),
##   ..   `2003` = col_character(),
##   ..   `2004` = col_character(),
##   ..   `2005` = col_character(),
##   ..   `2006` = col_character(),
##   ..   `2007` = col_character(),
##   ..   `2008` = col_character(),
##   ..   `2009` = col_character(),
##   ..   `2010` = col_character(),
##   ..   `2011` = col_character(),
##   ..   `2012` = col_character()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

2. Use `janitor` to rename the columns and make them easier to use. As part of this cleaning step, change `country`, `isscaap_group_number`, `asfis_species_number`, and `fao_major_fishing_area` to data class factor. 

```r
fisheries <- clean_names(fisheries)
```


```r
fisheries %>%
  mutate(across(c(country, isscaap_group_number, asfis_species_number, fao_major_fishing_area), as_factor))
```

```
## # A tibble: 17,692 × 71
##    country common_name               isscaap_group_number isscaap_taxonomic_gr…¹
##    <fct>   <chr>                     <fct>                <chr>                 
##  1 Albania Angelsharks, sand devils… 38                   Sharks, rays, chimaer…
##  2 Albania Atlantic bonito           36                   Tunas, bonitos, billf…
##  3 Albania Barracudas nei            37                   Miscellaneous pelagic…
##  4 Albania Blue and red shrimp       45                   Shrimps, prawns       
##  5 Albania Blue whiting(=Poutassou)  32                   Cods, hakes, haddocks 
##  6 Albania Bluefish                  37                   Miscellaneous pelagic…
##  7 Albania Bogue                     33                   Miscellaneous coastal…
##  8 Albania Caramote prawn            45                   Shrimps, prawns       
##  9 Albania Catsharks, nursehounds n… 38                   Sharks, rays, chimaer…
## 10 Albania Common cuttlefish         57                   Squids, cuttlefishes,…
## # ℹ 17,682 more rows
## # ℹ abbreviated name: ¹​isscaap_taxonomic_group
## # ℹ 67 more variables: asfis_species_number <fct>, asfis_species_name <chr>,
## #   fao_major_fishing_area <fct>, measure <chr>, x1950 <chr>, x1951 <chr>,
## #   x1952 <chr>, x1953 <chr>, x1954 <chr>, x1955 <chr>, x1956 <chr>,
## #   x1957 <chr>, x1958 <chr>, x1959 <chr>, x1960 <chr>, x1961 <chr>,
## #   x1962 <chr>, x1963 <chr>, x1964 <chr>, x1965 <chr>, x1966 <chr>, …
```

We need to deal with the years because they are being treated as characters and start with an X. We also have the problem that the column names that are years actually represent data. We haven't discussed tidy data yet, so here is some help. You should run this ugly chunk to transform the data for the rest of the homework. It will only work if you have used janitor to rename the variables in question 2!  

```r
fisheries_tidy <- fisheries %>% 
pivot_longer(-c(country,common_name,isscaap_group_number,isscaap_taxonomic_group,asfis_species_number,asfis_species_name,fao_major_fishing_area,measure),
              names_to = "year",
              values_to = "catch",
               values_drop_na = TRUE) %>% 
 mutate(year= as.numeric(str_replace(year, 'x', ''))) %>% 
  mutate(catch= str_replace(catch, c(' F'), replacement = '')) %>% 
 mutate(catch= str_replace(catch, c('...'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('-'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('0 0'), replacement = ''))

fisheries_tidy$catch <- as.numeric(fisheries_tidy$catch)
```

3. How many countries are represented in the data? Provide a count and list their names.

```r
fisheries_tidy %>% 
  summarize(ncountires = n_distinct(country))
```

```
## # A tibble: 1 × 1
##   ncountires
##        <int>
## 1        203
```

```r
unique(fisheries_tidy$country)
```

```
##   [1] "Albania"                   "Algeria"                  
##   [3] "American Samoa"            "Angola"                   
##   [5] "Anguilla"                  "Antigua and Barbuda"      
##   [7] "Argentina"                 "Aruba"                    
##   [9] "Australia"                 "Bahamas"                  
##  [11] "Bahrain"                   "Bangladesh"               
##  [13] "Barbados"                  "Belgium"                  
##  [15] "Belize"                    "Benin"                    
##  [17] "Bermuda"                   "Bonaire/S.Eustatius/Saba" 
##  [19] "Bosnia and Herzegovina"    "Brazil"                   
##  [21] "British Indian Ocean Ter"  "British Virgin Islands"   
##  [23] "Brunei Darussalam"         "Bulgaria"                 
##  [25] "Cabo Verde"                "Cambodia"                 
##  [27] "Cameroon"                  "Canada"                   
##  [29] "Cayman Islands"            "Channel Islands"          
##  [31] "Chile"                     "China"                    
##  [33] "China, Hong Kong SAR"      "China, Macao SAR"         
##  [35] "Colombia"                  "Comoros"                  
##  [37] "Congo, Dem. Rep. of the"   "Congo, Republic of"       
##  [39] "Cook Islands"              "Costa Rica"               
##  [41] "Croatia"                   "Cuba"                     
##  [43] "Cura\xe7ao"                "Cyprus"                   
##  [45] "C\xf4te d'Ivoire"          "Denmark"                  
##  [47] "Djibouti"                  "Dominica"                 
##  [49] "Dominican Republic"        "Ecuador"                  
##  [51] "Egypt"                     "El Salvador"              
##  [53] "Equatorial Guinea"         "Eritrea"                  
##  [55] "Estonia"                   "Ethiopia"                 
##  [57] "Falkland Is.(Malvinas)"    "Faroe Islands"            
##  [59] "Fiji, Republic of"         "Finland"                  
##  [61] "France"                    "French Guiana"            
##  [63] "French Polynesia"          "French Southern Terr"     
##  [65] "Gabon"                     "Gambia"                   
##  [67] "Georgia"                   "Germany"                  
##  [69] "Ghana"                     "Gibraltar"                
##  [71] "Greece"                    "Greenland"                
##  [73] "Grenada"                   "Guadeloupe"               
##  [75] "Guam"                      "Guatemala"                
##  [77] "Guinea"                    "GuineaBissau"             
##  [79] "Guyana"                    "Haiti"                    
##  [81] "Honduras"                  "Iceland"                  
##  [83] "India"                     "Indonesia"                
##  [85] "Iran (Islamic Rep. of)"    "Iraq"                     
##  [87] "Ireland"                   "Isle of Man"              
##  [89] "Israel"                    "Italy"                    
##  [91] "Jamaica"                   "Japan"                    
##  [93] "Jordan"                    "Kenya"                    
##  [95] "Kiribati"                  "Korea, Dem. People's Rep" 
##  [97] "Korea, Republic of"        "Kuwait"                   
##  [99] "Latvia"                    "Lebanon"                  
## [101] "Liberia"                   "Libya"                    
## [103] "Lithuania"                 "Madagascar"               
## [105] "Malaysia"                  "Maldives"                 
## [107] "Malta"                     "Marshall Islands"         
## [109] "Martinique"                "Mauritania"               
## [111] "Mauritius"                 "Mayotte"                  
## [113] "Mexico"                    "Micronesia, Fed.States of"
## [115] "Monaco"                    "Montenegro"               
## [117] "Montserrat"                "Morocco"                  
## [119] "Mozambique"                "Myanmar"                  
## [121] "Namibia"                   "Nauru"                    
## [123] "Netherlands"               "Netherlands Antilles"     
## [125] "New Caledonia"             "New Zealand"              
## [127] "Nicaragua"                 "Nigeria"                  
## [129] "Niue"                      "Norfolk Island"           
## [131] "Northern Mariana Is."      "Norway"                   
## [133] "Oman"                      "Other nei"                
## [135] "Pakistan"                  "Palau"                    
## [137] "Palestine, Occupied Tr."   "Panama"                   
## [139] "Papua New Guinea"          "Peru"                     
## [141] "Philippines"               "Pitcairn Islands"         
## [143] "Poland"                    "Portugal"                 
## [145] "Puerto Rico"               "Qatar"                    
## [147] "Romania"                   "Russian Federation"       
## [149] "R\xe9union"                "Saint Barth\xe9lemy"      
## [151] "Saint Helena"              "Saint Kitts and Nevis"    
## [153] "Saint Lucia"               "Saint Vincent/Grenadines" 
## [155] "SaintMartin"               "Samoa"                    
## [157] "Sao Tome and Principe"     "Saudi Arabia"             
## [159] "Senegal"                   "Serbia and Montenegro"    
## [161] "Seychelles"                "Sierra Leone"             
## [163] "Singapore"                 "Sint Maarten"             
## [165] "Slovenia"                  "Solomon Islands"          
## [167] "Somalia"                   "South Africa"             
## [169] "Spain"                     "Sri Lanka"                
## [171] "St. Pierre and Miquelon"   "Sudan"                    
## [173] "Sudan (former)"            "Suriname"                 
## [175] "Svalbard and Jan Mayen"    "Sweden"                   
## [177] "Syrian Arab Republic"      "Taiwan Province of China" 
## [179] "Tanzania, United Rep. of"  "Thailand"                 
## [181] "TimorLeste"                "Togo"                     
## [183] "Tokelau"                   "Tonga"                    
## [185] "Trinidad and Tobago"       "Tunisia"                  
## [187] "Turkey"                    "Turks and Caicos Is."     
## [189] "Tuvalu"                    "US Virgin Islands"        
## [191] "Ukraine"                   "Un. Sov. Soc. Rep."       
## [193] "United Arab Emirates"      "United Kingdom"           
## [195] "United States of America"  "Uruguay"                  
## [197] "Vanuatu"                   "Venezuela, Boliv Rep of"  
## [199] "Viet Nam"                  "Wallis and Futuna Is."    
## [201] "Yemen"                     "Yugoslavia SFR"           
## [203] "Zanzibar"
```

4. Refocus the data only to include country, isscaap_taxonomic_group, asfis_species_name, asfis_species_number, year, catch.

```r
fishers_new <- fisheries_tidy %>%
  select(country, isscaap_taxonomic_group, asfis_species_name, asfis_species_number, year, catch)
fishers_new
```

```
## # A tibble: 376,771 × 6
##    country isscaap_taxonomic_group asfis_species_name asfis_species_number  year
##    <chr>   <chr>                   <chr>              <chr>                <dbl>
##  1 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            1995
##  2 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            1996
##  3 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            1997
##  4 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            1998
##  5 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            1999
##  6 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            2000
##  7 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            2001
##  8 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            2002
##  9 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            2003
## 10 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX            2004
## # ℹ 376,761 more rows
## # ℹ 1 more variable: catch <dbl>
```

5. Based on the asfis_species_number, how many distinct fish species were caught as part of these data?

```r
fishers_new %>% 
  summarize(n_taxa=n_distinct(asfis_species_number))
```

```
## # A tibble: 1 × 1
##   n_taxa
##    <int>
## 1   1551
```

6. Which country had the largest overall catch in the year 2000?

```r
fisheries_tidy %>% 
  filter(year==2000) %>%
  group_by(country) %>% 
  summarize(catch_total=sum(catch, na.rm=T)) %>% 
  arrange(desc(catch_total))
```

```
## # A tibble: 193 × 2
##    country                  catch_total
##    <chr>                          <dbl>
##  1 China                          25899
##  2 Russian Federation             12181
##  3 United States of America       11762
##  4 Japan                           8510
##  5 Indonesia                       8341
##  6 Peru                            7443
##  7 Chile                           6906
##  8 India                           6351
##  9 Thailand                        6243
## 10 Korea, Republic of              6124
## # ℹ 183 more rows
```

7. Which country caught the most sardines (_Sardina pilchardus_) between the years 1990-2000?

```r
fisheries_tidy %>%
  filter(asfis_species_name== "Sardina pilchardus") %>%
  filter(year>=1990 & year<=2000) %>%
  group_by(country) %>%
  summarize(catch_total=sum(catch, na.rm=T)) %>%
  arrange(desc(catch_total))
```

```
## # A tibble: 37 × 2
##    country               catch_total
##    <chr>                       <dbl>
##  1 Morocco                      7470
##  2 Spain                        3507
##  3 Russian Federation           1639
##  4 Ukraine                      1030
##  5 France                        966
##  6 Portugal                      818
##  7 Greece                        528
##  8 Italy                         507
##  9 Serbia and Montenegro         478
## 10 Denmark                       477
## # ℹ 27 more rows
```

8. Which five countries caught the most cephalopods between 2008-2012?

```r
fishers_new %>%
  filter(str_detect(isscaap_taxonomic_group, "Squids"))%>%
  filter(year>=2008 & year<=2012) %>%
  group_by(country) %>% 
  summarize(catch_total=sum(catch, na.rm=T)) %>% 
  arrange(desc(catch_total))
```

```
## # A tibble: 122 × 2
##    country                  catch_total
##    <chr>                          <dbl>
##  1 China                           8349
##  2 Korea, Republic of              3480
##  3 Peru                            3422
##  4 Japan                           3248
##  5 Chile                           2775
##  6 United States of America        2417
##  7 Indonesia                       1622
##  8 Taiwan Province of China        1394
##  9 Spain                           1147
## 10 France                          1138
## # ℹ 112 more rows
```

9. Which species had the highest catch total between 2008-2012? (hint: Osteichthyes is not a species)

```r
fishers_new %>%
  filter(year>=2008 & year>=2012) %>%
  group_by(asfis_species_name) %>% 
  summarize(catch_total=sum(catch, na.rm=T)) %>%
   arrange(desc(catch_total))
```

```
## # A tibble: 1,396 × 2
##    asfis_species_name    catch_total
##    <chr>                       <dbl>
##  1 Osteichthyes                19018
##  2 Theragra chalcogramma       11856
##  3 Engraulis ringens            7755
##  4 Katsuwonus pelamis           7673
##  5 Trichiurus lepturus          7309
##  6 Thunnus albacares            4509
##  7 Clupea harengus              3719
##  8 Gadus morhua                 3036
##  9 Scomber japonicus            2888
## 10 Scomber scombrus             2287
## # ℹ 1,386 more rows
```

10. Use the data to do at least one analysis of your choice.

```r
fishers_new %>%
  group_by(asfis_species_name) %>% 
  summarize(catch_total=mean(catch, na.rm=T)) %>%
   arrange(desc(catch_total))
```

```
## # A tibble: 1,546 × 2
##    asfis_species_name      catch_total
##    <chr>                         <dbl>
##  1 Engraulis ringens             4097.
##  2 Sardinops sagax               1314.
##  3 Theragra chalcogramma         1084.
##  4 Sardinops melanostictus       1012.
##  5 Trachurus murphyi              549.
##  6 Brevoortia patronus            523.
##  7 Engraulis japonicus            487.
##  8 Spisula solidissima            362.
##  9 Engraulis capensis             343.
## 10 Chelon haematocheilus          339 
## # ℹ 1,536 more rows
```

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
