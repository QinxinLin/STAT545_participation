cm005-exercise
================

``` r
library(gapminder)
library(tidyverse)
```

    ## ── Attaching packages ───────────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 3.0.0     ✔ purrr   0.2.5
    ## ✔ tibble  1.4.2     ✔ dplyr   0.7.6
    ## ✔ tidyr   0.8.1     ✔ stringr 1.3.1
    ## ✔ readr   1.1.1     ✔ forcats 0.3.0

    ## ── Conflicts ──────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

## select

``` r
select(gapminder,year,lifeExp,country)
```

    ## # A tibble: 1,704 x 3
    ##     year lifeExp country    
    ##    <int>   <dbl> <fct>      
    ##  1  1952    28.8 Afghanistan
    ##  2  1957    30.3 Afghanistan
    ##  3  1962    32.0 Afghanistan
    ##  4  1967    34.0 Afghanistan
    ##  5  1972    36.1 Afghanistan
    ##  6  1977    38.4 Afghanistan
    ##  7  1982    39.9 Afghanistan
    ##  8  1987    40.8 Afghanistan
    ##  9  1992    41.7 Afghanistan
    ## 10  1997    41.8 Afghanistan
    ## # ... with 1,694 more rows

``` r
select(gapminder,country:lifeExp)
```

    ## # A tibble: 1,704 x 4
    ##    country     continent  year lifeExp
    ##    <fct>       <fct>     <int>   <dbl>
    ##  1 Afghanistan Asia       1952    28.8
    ##  2 Afghanistan Asia       1957    30.3
    ##  3 Afghanistan Asia       1962    32.0
    ##  4 Afghanistan Asia       1967    34.0
    ##  5 Afghanistan Asia       1972    36.1
    ##  6 Afghanistan Asia       1977    38.4
    ##  7 Afghanistan Asia       1982    39.9
    ##  8 Afghanistan Asia       1987    40.8
    ##  9 Afghanistan Asia       1992    41.7
    ## 10 Afghanistan Asia       1997    41.8
    ## # ... with 1,694 more rows

``` r
select(gapminder,-lifeExp)
```

    ## # A tibble: 1,704 x 5
    ##    country     continent  year      pop gdpPercap
    ##    <fct>       <fct>     <int>    <int>     <dbl>
    ##  1 Afghanistan Asia       1952  8425333      779.
    ##  2 Afghanistan Asia       1957  9240934      821.
    ##  3 Afghanistan Asia       1962 10267083      853.
    ##  4 Afghanistan Asia       1967 11537966      836.
    ##  5 Afghanistan Asia       1972 13079460      740.
    ##  6 Afghanistan Asia       1977 14880372      786.
    ##  7 Afghanistan Asia       1982 12881816      978.
    ##  8 Afghanistan Asia       1987 13867957      852.
    ##  9 Afghanistan Asia       1992 16317921      649.
    ## 10 Afghanistan Asia       1997 22227415      635.
    ## # ... with 1,694 more rows

``` r
select(gapminder,continent,everything())
```

    ## # A tibble: 1,704 x 6
    ##    continent country      year lifeExp      pop gdpPercap
    ##    <fct>     <fct>       <int>   <dbl>    <int>     <dbl>
    ##  1 Asia      Afghanistan  1952    28.8  8425333      779.
    ##  2 Asia      Afghanistan  1957    30.3  9240934      821.
    ##  3 Asia      Afghanistan  1962    32.0 10267083      853.
    ##  4 Asia      Afghanistan  1967    34.0 11537966      836.
    ##  5 Asia      Afghanistan  1972    36.1 13079460      740.
    ##  6 Asia      Afghanistan  1977    38.4 14880372      786.
    ##  7 Asia      Afghanistan  1982    39.9 12881816      978.
    ##  8 Asia      Afghanistan  1987    40.8 13867957      852.
    ##  9 Asia      Afghanistan  1992    41.7 16317921      649.
    ## 10 Asia      Afghanistan  1997    41.8 22227415      635.
    ## # ... with 1,694 more rows

``` r
rename(gapminder,cont=continent)
```

    ## # A tibble: 1,704 x 6
    ##    country     cont   year lifeExp      pop gdpPercap
    ##    <fct>       <fct> <int>   <dbl>    <int>     <dbl>
    ##  1 Afghanistan Asia   1952    28.8  8425333      779.
    ##  2 Afghanistan Asia   1957    30.3  9240934      821.
    ##  3 Afghanistan Asia   1962    32.0 10267083      853.
    ##  4 Afghanistan Asia   1967    34.0 11537966      836.
    ##  5 Afghanistan Asia   1972    36.1 13079460      740.
    ##  6 Afghanistan Asia   1977    38.4 14880372      786.
    ##  7 Afghanistan Asia   1982    39.9 12881816      978.
    ##  8 Afghanistan Asia   1987    40.8 13867957      852.
    ##  9 Afghanistan Asia   1992    41.7 16317921      649.
    ## 10 Afghanistan Asia   1997    41.8 22227415      635.
    ## # ... with 1,694 more rows

## arrange

``` r
arrange(gapminder,year)
```

    ## # A tibble: 1,704 x 6
    ##    country     continent  year lifeExp      pop gdpPercap
    ##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
    ##  1 Afghanistan Asia       1952    28.8  8425333      779.
    ##  2 Albania     Europe     1952    55.2  1282697     1601.
    ##  3 Algeria     Africa     1952    43.1  9279525     2449.
    ##  4 Angola      Africa     1952    30.0  4232095     3521.
    ##  5 Argentina   Americas   1952    62.5 17876956     5911.
    ##  6 Australia   Oceania    1952    69.1  8691212    10040.
    ##  7 Austria     Europe     1952    66.8  6927772     6137.
    ##  8 Bahrain     Asia       1952    50.9   120447     9867.
    ##  9 Bangladesh  Asia       1952    37.5 46886859      684.
    ## 10 Belgium     Europe     1952    68    8730405     8343.
    ## # ... with 1,694 more rows

``` r
arrange(gapminder,desc(year))
```

    ## # A tibble: 1,704 x 6
    ##    country     continent  year lifeExp       pop gdpPercap
    ##    <fct>       <fct>     <int>   <dbl>     <int>     <dbl>
    ##  1 Afghanistan Asia       2007    43.8  31889923      975.
    ##  2 Albania     Europe     2007    76.4   3600523     5937.
    ##  3 Algeria     Africa     2007    72.3  33333216     6223.
    ##  4 Angola      Africa     2007    42.7  12420476     4797.
    ##  5 Argentina   Americas   2007    75.3  40301927    12779.
    ##  6 Australia   Oceania    2007    81.2  20434176    34435.
    ##  7 Austria     Europe     2007    79.8   8199783    36126.
    ##  8 Bahrain     Asia       2007    75.6    708573    29796.
    ##  9 Bangladesh  Asia       2007    64.1 150448339     1391.
    ## 10 Belgium     Europe     2007    79.4  10392226    33693.
    ## # ... with 1,694 more rows

``` r
arrange(gapminder,year,lifeExp)
```

    ## # A tibble: 1,704 x 6
    ##    country       continent  year lifeExp     pop gdpPercap
    ##    <fct>         <fct>     <int>   <dbl>   <int>     <dbl>
    ##  1 Afghanistan   Asia       1952    28.8 8425333      779.
    ##  2 Gambia        Africa     1952    30    284320      485.
    ##  3 Angola        Africa     1952    30.0 4232095     3521.
    ##  4 Sierra Leone  Africa     1952    30.3 2143249      880.
    ##  5 Mozambique    Africa     1952    31.3 6446316      469.
    ##  6 Burkina Faso  Africa     1952    32.0 4469979      543.
    ##  7 Guinea-Bissau Africa     1952    32.5  580653      300.
    ##  8 Yemen, Rep.   Asia       1952    32.5 4963829      782.
    ##  9 Somalia       Africa     1952    33.0 2526994     1136.
    ## 10 Guinea        Africa     1952    33.6 2664249      510.
    ## # ... with 1,694 more rows

## filter

``` r
filter(gapminder,pop>1000000)
```

    ## # A tibble: 1,524 x 6
    ##    country     continent  year lifeExp      pop gdpPercap
    ##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
    ##  1 Afghanistan Asia       1952    28.8  8425333      779.
    ##  2 Afghanistan Asia       1957    30.3  9240934      821.
    ##  3 Afghanistan Asia       1962    32.0 10267083      853.
    ##  4 Afghanistan Asia       1967    34.0 11537966      836.
    ##  5 Afghanistan Asia       1972    36.1 13079460      740.
    ##  6 Afghanistan Asia       1977    38.4 14880372      786.
    ##  7 Afghanistan Asia       1982    39.9 12881816      978.
    ##  8 Afghanistan Asia       1987    40.8 13867957      852.
    ##  9 Afghanistan Asia       1992    41.7 16317921      649.
    ## 10 Afghanistan Asia       1997    41.8 22227415      635.
    ## # ... with 1,514 more rows

``` r
filter(gapminder,continent=="Asia")
```

    ## # A tibble: 396 x 6
    ##    country     continent  year lifeExp      pop gdpPercap
    ##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
    ##  1 Afghanistan Asia       1952    28.8  8425333      779.
    ##  2 Afghanistan Asia       1957    30.3  9240934      821.
    ##  3 Afghanistan Asia       1962    32.0 10267083      853.
    ##  4 Afghanistan Asia       1967    34.0 11537966      836.
    ##  5 Afghanistan Asia       1972    36.1 13079460      740.
    ##  6 Afghanistan Asia       1977    38.4 14880372      786.
    ##  7 Afghanistan Asia       1982    39.9 12881816      978.
    ##  8 Afghanistan Asia       1987    40.8 13867957      852.
    ##  9 Afghanistan Asia       1992    41.7 16317921      649.
    ## 10 Afghanistan Asia       1997    41.8 22227415      635.
    ## # ... with 386 more rows
