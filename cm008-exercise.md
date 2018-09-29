Cm008-exercise
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

## mutate

``` r
gapminder %>%
  mutate(gdp=gdpPercap*pop,
         gdpBill=round(gdp/10^9,2))
```

    ## # A tibble: 1,704 x 8
    ##    country    continent  year lifeExp     pop gdpPercap        gdp gdpBill
    ##    <fct>      <fct>     <int>   <dbl>   <int>     <dbl>      <dbl>   <dbl>
    ##  1 Afghanist… Asia       1952    28.8  8.43e6      779.    6.57e 9    6.57
    ##  2 Afghanist… Asia       1957    30.3  9.24e6      821.    7.59e 9    7.59
    ##  3 Afghanist… Asia       1962    32.0  1.03e7      853.    8.76e 9    8.76
    ##  4 Afghanist… Asia       1967    34.0  1.15e7      836.    9.65e 9    9.65
    ##  5 Afghanist… Asia       1972    36.1  1.31e7      740.    9.68e 9    9.68
    ##  6 Afghanist… Asia       1977    38.4  1.49e7      786.    1.17e10   11.7 
    ##  7 Afghanist… Asia       1982    39.9  1.29e7      978.    1.26e10   12.6 
    ##  8 Afghanist… Asia       1987    40.8  1.39e7      852.    1.18e10   11.8 
    ##  9 Afghanist… Asia       1992    41.7  1.63e7      649.    1.06e10   10.6 
    ## 10 Afghanist… Asia       1997    41.8  2.22e7      635.    1.41e10   14.1 
    ## # ... with 1,694 more rows

``` r
gapminder %>%
  mutate(lifeExp=if_else(country=="Canada"&year==1952,70,lifeExp))%>%
  filter(country=="Canada")
```

    ## # A tibble: 12 x 6
    ##    country continent  year lifeExp      pop gdpPercap
    ##    <fct>   <fct>     <int>   <dbl>    <int>     <dbl>
    ##  1 Canada  Americas   1952    70   14785584    11367.
    ##  2 Canada  Americas   1957    70.0 17010154    12490.
    ##  3 Canada  Americas   1962    71.3 18985849    13462.
    ##  4 Canada  Americas   1967    72.1 20819767    16077.
    ##  5 Canada  Americas   1972    72.9 22284500    18971.
    ##  6 Canada  Americas   1977    74.2 23796400    22091.
    ##  7 Canada  Americas   1982    75.8 25201900    22899.
    ##  8 Canada  Americas   1987    76.9 26549700    26627.
    ##  9 Canada  Americas   1992    78.0 28523502    26343.
    ## 10 Canada  Americas   1997    78.6 30305843    28955.
    ## 11 Canada  Americas   2002    79.8 31902268    33329.
    ## 12 Canada  Americas   2007    80.7 33390141    36319.

``` r
filter(gapminder,country=="Canada")
```

    ## # A tibble: 12 x 6
    ##    country continent  year lifeExp      pop gdpPercap
    ##    <fct>   <fct>     <int>   <dbl>    <int>     <dbl>
    ##  1 Canada  Americas   1952    68.8 14785584    11367.
    ##  2 Canada  Americas   1957    70.0 17010154    12490.
    ##  3 Canada  Americas   1962    71.3 18985849    13462.
    ##  4 Canada  Americas   1967    72.1 20819767    16077.
    ##  5 Canada  Americas   1972    72.9 22284500    18971.
    ##  6 Canada  Americas   1977    74.2 23796400    22091.
    ##  7 Canada  Americas   1982    75.8 25201900    22899.
    ##  8 Canada  Americas   1987    76.9 26549700    26627.
    ##  9 Canada  Americas   1992    78.0 28523502    26343.
    ## 10 Canada  Americas   1997    78.6 30305843    28955.
    ## 11 Canada  Americas   2002    79.8 31902268    33329.
    ## 12 Canada  Americas   2007    80.7 33390141    36319.

``` r
gapminder%>%
  mutate(cc=paste(country,continent,sep=", "))
```

    ## # A tibble: 1,704 x 7
    ##    country     continent  year lifeExp      pop gdpPercap cc               
    ##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl> <chr>            
    ##  1 Afghanistan Asia       1952    28.8  8425333      779. Afghanistan, Asia
    ##  2 Afghanistan Asia       1957    30.3  9240934      821. Afghanistan, Asia
    ##  3 Afghanistan Asia       1962    32.0 10267083      853. Afghanistan, Asia
    ##  4 Afghanistan Asia       1967    34.0 11537966      836. Afghanistan, Asia
    ##  5 Afghanistan Asia       1972    36.1 13079460      740. Afghanistan, Asia
    ##  6 Afghanistan Asia       1977    38.4 14880372      786. Afghanistan, Asia
    ##  7 Afghanistan Asia       1982    39.9 12881816      978. Afghanistan, Asia
    ##  8 Afghanistan Asia       1987    40.8 13867957      852. Afghanistan, Asia
    ##  9 Afghanistan Asia       1992    41.7 16317921      649. Afghanistan, Asia
    ## 10 Afghanistan Asia       1997    41.8 22227415      635. Afghanistan, Asia
    ## # ... with 1,694 more rows

## summarize and group\_by

``` r
gapminder%>%
  summarize(me = mean(lifeExp),
            med = median(lifeExp))
```

    ## # A tibble: 1 x 2
    ##      me   med
    ##   <dbl> <dbl>
    ## 1  59.5  60.7

``` r
gapminder%>%
  group_by(continent,country)%>%
  summarize(med=median(gdpPercap))%>%
  summarize(me=median(med))
```

    ## # A tibble: 5 x 2
    ##   continent     me
    ##   <fct>      <dbl>
    ## 1 Africa     1193.
    ## 2 Americas   5891.
    ## 3 Asia       3142.
    ## 4 Europe    14640.
    ## 5 Oceania   17919.

``` r
gapminder%>%
  mutate(hvsl=if_else(lifeExp>60,"high","low"))%>%
  group_by(continent,hvsl)%>%
  summarize(med=median(gdpPercap))
```

    ## # A tibble: 9 x 3
    ## # Groups:   continent [?]
    ##   continent hvsl     med
    ##   <fct>     <chr>  <dbl>
    ## 1 Africa    high   4442.
    ## 2 Africa    low    1071.
    ## 3 Americas  high   6678.
    ## 4 Americas  low    3080.
    ## 5 Asia      high   5250.
    ## 6 Asia      low    1031.
    ## 7 Europe    high  12672.
    ## 8 Europe    low    2384.
    ## 9 Oceania   high  17983.

``` r
gapminder%>%
  group_by(continent)%>%
  summarize(n=n_distinct(country))
```

    ## # A tibble: 5 x 2
    ##   continent     n
    ##   <fct>     <int>
    ## 1 Africa       52
    ## 2 Americas     25
    ## 3 Asia         33
    ## 4 Europe       30
    ## 5 Oceania       2

## grouped mutate

``` r
gapminder%>%
  group_by(country)%>%
  mutate(growth=pop-first(pop))
```

    ## # A tibble: 1,704 x 7
    ## # Groups:   country [142]
    ##    country     continent  year lifeExp      pop gdpPercap   growth
    ##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>    <int>
    ##  1 Afghanistan Asia       1952    28.8  8425333      779.        0
    ##  2 Afghanistan Asia       1957    30.3  9240934      821.   815601
    ##  3 Afghanistan Asia       1962    32.0 10267083      853.  1841750
    ##  4 Afghanistan Asia       1967    34.0 11537966      836.  3112633
    ##  5 Afghanistan Asia       1972    36.1 13079460      740.  4654127
    ##  6 Afghanistan Asia       1977    38.4 14880372      786.  6455039
    ##  7 Afghanistan Asia       1982    39.9 12881816      978.  4456483
    ##  8 Afghanistan Asia       1987    40.8 13867957      852.  5442624
    ##  9 Afghanistan Asia       1992    41.7 16317921      649.  7892588
    ## 10 Afghanistan Asia       1997    41.8 22227415      635. 13802082
    ## # ... with 1,694 more rows

``` r
gapminder%>%
  group_by(country)%>%
  mutate(growth=pop-pop[year==1972])
```

    ## # A tibble: 1,704 x 7
    ## # Groups:   country [142]
    ##    country     continent  year lifeExp      pop gdpPercap   growth
    ##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>    <int>
    ##  1 Afghanistan Asia       1952    28.8  8425333      779. -4654127
    ##  2 Afghanistan Asia       1957    30.3  9240934      821. -3838526
    ##  3 Afghanistan Asia       1962    32.0 10267083      853. -2812377
    ##  4 Afghanistan Asia       1967    34.0 11537966      836. -1541494
    ##  5 Afghanistan Asia       1972    36.1 13079460      740.        0
    ##  6 Afghanistan Asia       1977    38.4 14880372      786.  1800912
    ##  7 Afghanistan Asia       1982    39.9 12881816      978.  -197644
    ##  8 Afghanistan Asia       1987    40.8 13867957      852.   788497
    ##  9 Afghanistan Asia       1992    41.7 16317921      649.  3238461
    ## 10 Afghanistan Asia       1997    41.8 22227415      635.  9147955
    ## # ... with 1,694 more rows

``` r
group_by(gapminder, continent, country)%>%
  mutate(l=lifeExp-lag(lifeExp))%>%
  summarize(n=min(l,na.rm=TRUE))%>%
  top_n(1, wt=desc(n))%>%
  arrange(n)
```

    ## # A tibble: 5 x 3
    ## # Groups:   continent [5]
    ##   continent country           n
    ##   <fct>     <fct>         <dbl>
    ## 1 Africa    Rwanda      -20.4  
    ## 2 Asia      Cambodia     -9.10 
    ## 3 Americas  El Salvador  -1.51 
    ## 4 Europe    Montenegro   -1.46 
    ## 5 Oceania   Australia     0.170
