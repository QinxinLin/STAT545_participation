Cm006-exercise
================

``` r
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

``` r
library(gapminder)
library(scales)
```

    ## 
    ## Attaching package: 'scales'

    ## The following object is masked from 'package:purrr':
    ## 
    ##     discard

    ## The following object is masked from 'package:readr':
    ## 
    ##     col_factor

## scatterplot

``` r
ggplot(data=gapminder,aes(x=gdpPercap, y = lifeExp)) + geom_point()
```

![](cm006-exercise_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

## histogram and density plot

``` r
ggplot(data=gapminder,aes(x=lifeExp)) + geom_histogram(bandwith=50) 
```

    ## Warning: Ignoring unknown parameters: bandwith

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](cm006-exercise_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

``` r
ggplot(data=gapminder,aes(x=lifeExp)) + geom_density() 
```

![](cm006-exercise_files/figure-gfm/unnamed-chunk-3-2.png)<!-- -->

## box and violin

``` r
ggplot(data=gapminder,aes(x=continent,y=log(pop)))+geom_boxplot()
```

![](cm006-exercise_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

``` r
ggplot(data=gapminder,aes(x=continent,y=log(pop)))+geom_violin()
```

![](cm006-exercise_files/figure-gfm/unnamed-chunk-4-2.png)<!-- -->

## jitter plot

``` r
ggplot(data=gapminder,aes(x=continent,y=log(pop)))+
  geom_point()+
   geom_jitter()
```

![](cm006-exercise_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

## time/line plot

``` r
filter(gapminder,country=="Canada") %>%
  ggplot(aes(x=year,y=lifeExp))+geom_point()
```

![](cm006-exercise_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r
ggplot(gapminder,aes(x=country,y=lifeExp))+geom_line()
```

![](cm006-exercise_files/figure-gfm/unnamed-chunk-6-2.png)<!-- -->

## path plot

``` r
ggplot(gapminder,aes(x=gdpPercap,y=lifeExp))+geom_point()+geom_line()
```

![](cm006-exercise_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

## Bar plot

``` r
f<-filter(gapminder,year==2007)%>%group_by(continent)%>%
    summarise(count=n())%>%mutate(pct=count/sum(count))
ggplot(f,aes(x=continent,y=pct))+geom_bar(stat="identity")
```

![](cm006-exercise_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->
