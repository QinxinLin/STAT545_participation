Cm009-exercise
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

``` r
tibble(x=1:5,
       y=1,
       z=x^2+y)
```

    ## # A tibble: 5 x 3
    ##       x     y     z
    ##   <int> <dbl> <dbl>
    ## 1     1     1     2
    ## 2     2     1     5
    ## 3     3     1    10
    ## 4     4     1    17
    ## 5     5     1    26

``` r
tribble(
  ~x,~y,~z,
  1,2,3,
  4,5,6)
```

    ## # A tibble: 2 x 3
    ##       x     y     z
    ##   <dbl> <dbl> <dbl>
    ## 1     1     2     3
    ## 2     4     5     6

``` r
write_delim(iris,"iris.txt",delim="$")
read_delim("iris.txt",delim = "$")
```

    ## Parsed with column specification:
    ## cols(
    ##   Sepal.Length = col_double(),
    ##   Sepal.Width = col_double(),
    ##   Petal.Length = col_double(),
    ##   Petal.Width = col_double(),
    ##   Species = col_character()
    ## )

    ## # A tibble: 150 x 5
    ##    Sepal.Length Sepal.Width Petal.Length Petal.Width Species
    ##           <dbl>       <dbl>        <dbl>       <dbl> <chr>  
    ##  1          5.1         3.5          1.4         0.2 setosa 
    ##  2          4.9         3            1.4         0.2 setosa 
    ##  3          4.7         3.2          1.3         0.2 setosa 
    ##  4          4.6         3.1          1.5         0.2 setosa 
    ##  5          5           3.6          1.4         0.2 setosa 
    ##  6          5.4         3.9          1.7         0.4 setosa 
    ##  7          4.6         3.4          1.4         0.3 setosa 
    ##  8          5           3.4          1.5         0.2 setosa 
    ##  9          4.4         2.9          1.4         0.2 setosa 
    ## 10          4.9         3.1          1.5         0.1 setosa 
    ## # ... with 140 more rows

``` r
lotr1<-read_csv("https://raw.githubusercontent.com/jennybc/lotr-tidy/master/data/The_Fellowship_Of_The_Ring.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   Film = col_character(),
    ##   Race = col_character(),
    ##   Female = col_integer(),
    ##   Male = col_integer()
    ## )

``` r
lotr2<-read_csv("https://raw.githubusercontent.com/jennybc/lotr-tidy/master/data/The_Two_Towers.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   Film = col_character(),
    ##   Race = col_character(),
    ##   Female = col_integer(),
    ##   Male = col_integer()
    ## )

``` r
lotr3<-read_csv("https://raw.githubusercontent.com/jennybc/lotr-tidy/master/data/The_Return_Of_The_King.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   Film = col_character(),
    ##   Race = col_character(),
    ##   Female = col_integer(),
    ##   Male = col_integer()
    ## )

``` r
lotr1
```

    ## # A tibble: 3 x 4
    ##   Film                       Race   Female  Male
    ##   <chr>                      <chr>   <int> <int>
    ## 1 The Fellowship Of The Ring Elf      1229   971
    ## 2 The Fellowship Of The Ring Hobbit     14  3644
    ## 3 The Fellowship Of The Ring Man         0  1995

``` r
lotr2
```

    ## # A tibble: 3 x 4
    ##   Film           Race   Female  Male
    ##   <chr>          <chr>   <int> <int>
    ## 1 The Two Towers Elf       331   513
    ## 2 The Two Towers Hobbit      0  2463
    ## 3 The Two Towers Man       401  3589

``` r
lotr3
```

    ## # A tibble: 3 x 4
    ##   Film                   Race   Female  Male
    ##   <chr>                  <chr>   <int> <int>
    ## 1 The Return Of The King Elf       183   510
    ## 2 The Return Of The King Hobbit      2  2673
    ## 3 The Return Of The King Man       268  2459

``` r
lotr<-bind_rows(lotr1,lotr2,lotr3)
gather(lotr,key = "gender", value = "word", Female:Male)
```

    ## # A tibble: 18 x 4
    ##    Film                       Race   gender  word
    ##    <chr>                      <chr>  <chr>  <int>
    ##  1 The Fellowship Of The Ring Elf    Female  1229
    ##  2 The Fellowship Of The Ring Hobbit Female    14
    ##  3 The Fellowship Of The Ring Man    Female     0
    ##  4 The Two Towers             Elf    Female   331
    ##  5 The Two Towers             Hobbit Female     0
    ##  6 The Two Towers             Man    Female   401
    ##  7 The Return Of The King     Elf    Female   183
    ##  8 The Return Of The King     Hobbit Female     2
    ##  9 The Return Of The King     Man    Female   268
    ## 10 The Fellowship Of The Ring Elf    Male     971
    ## 11 The Fellowship Of The Ring Hobbit Male    3644
    ## 12 The Fellowship Of The Ring Man    Male    1995
    ## 13 The Two Towers             Elf    Male     513
    ## 14 The Two Towers             Hobbit Male    2463
    ## 15 The Two Towers             Man    Male    3589
    ## 16 The Return Of The King     Elf    Male     510
    ## 17 The Return Of The King     Hobbit Male    2673
    ## 18 The Return Of The King     Man    Male    2459

``` r
gather(lotr, key = "gender", value = "word", contains("ale"))
```

    ## # A tibble: 18 x 4
    ##    Film                       Race   gender  word
    ##    <chr>                      <chr>  <chr>  <int>
    ##  1 The Fellowship Of The Ring Elf    Female  1229
    ##  2 The Fellowship Of The Ring Hobbit Female    14
    ##  3 The Fellowship Of The Ring Man    Female     0
    ##  4 The Two Towers             Elf    Female   331
    ##  5 The Two Towers             Hobbit Female     0
    ##  6 The Two Towers             Man    Female   401
    ##  7 The Return Of The King     Elf    Female   183
    ##  8 The Return Of The King     Hobbit Female     2
    ##  9 The Return Of The King     Man    Female   268
    ## 10 The Fellowship Of The Ring Elf    Male     971
    ## 11 The Fellowship Of The Ring Hobbit Male    3644
    ## 12 The Fellowship Of The Ring Man    Male    1995
    ## 13 The Two Towers             Elf    Male     513
    ## 14 The Two Towers             Hobbit Male    2463
    ## 15 The Two Towers             Man    Male    3589
    ## 16 The Return Of The King     Elf    Male     510
    ## 17 The Return Of The King     Hobbit Male    2673
    ## 18 The Return Of The King     Man    Male    2459

``` r
list1<-list(lotr1, lotr2, lotr3)
do.call(bind_rows,list1)
```

    ## # A tibble: 9 x 4
    ##   Film                       Race   Female  Male
    ##   <chr>                      <chr>   <int> <int>
    ## 1 The Fellowship Of The Ring Elf      1229   971
    ## 2 The Fellowship Of The Ring Hobbit     14  3644
    ## 3 The Fellowship Of The Ring Man         0  1995
    ## 4 The Two Towers             Elf       331   513
    ## 5 The Two Towers             Hobbit      0  2463
    ## 6 The Two Towers             Man       401  3589
    ## 7 The Return Of The King     Elf       183   510
    ## 8 The Return Of The King     Hobbit      2  2673
    ## 9 The Return Of The King     Man       268  2459

``` r
lotr_tidy<-read_csv("https://raw.githubusercontent.com/jennybc/lotr-tidy/master/data/lotr_tidy.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   Film = col_character(),
    ##   Race = col_character(),
    ##   Gender = col_character(),
    ##   Words = col_integer()
    ## )

``` r
a<-spread(lotr_tidy,key = "Race", value = "Words")
gather(a,key="race",value="value",Elf:Man )
```

    ## # A tibble: 18 x 4
    ##    Film                       Gender race   value
    ##    <chr>                      <chr>  <chr>  <int>
    ##  1 The Fellowship Of The Ring Female Elf     1229
    ##  2 The Fellowship Of The Ring Male   Elf      971
    ##  3 The Return Of The King     Female Elf      183
    ##  4 The Return Of The King     Male   Elf      510
    ##  5 The Two Towers             Female Elf      331
    ##  6 The Two Towers             Male   Elf      513
    ##  7 The Fellowship Of The Ring Female Hobbit    14
    ##  8 The Fellowship Of The Ring Male   Hobbit  3644
    ##  9 The Return Of The King     Female Hobbit     2
    ## 10 The Return Of The King     Male   Hobbit  2673
    ## 11 The Two Towers             Female Hobbit     0
    ## 12 The Two Towers             Male   Hobbit  2463
    ## 13 The Fellowship Of The Ring Female Man        0
    ## 14 The Fellowship Of The Ring Male   Man     1995
    ## 15 The Return Of The King     Female Man      268
    ## 16 The Return Of The King     Male   Man     2459
    ## 17 The Two Towers             Female Man      401
    ## 18 The Two Towers             Male   Man     3589

``` r
lotr_tidy
```

    ## # A tibble: 18 x 4
    ##    Film                       Race   Gender Words
    ##    <chr>                      <chr>  <chr>  <int>
    ##  1 The Fellowship Of The Ring Elf    Female  1229
    ##  2 The Fellowship Of The Ring Hobbit Female    14
    ##  3 The Fellowship Of The Ring Man    Female     0
    ##  4 The Two Towers             Elf    Female   331
    ##  5 The Two Towers             Hobbit Female     0
    ##  6 The Two Towers             Man    Female   401
    ##  7 The Return Of The King     Elf    Female   183
    ##  8 The Return Of The King     Hobbit Female     2
    ##  9 The Return Of The King     Man    Female   268
    ## 10 The Fellowship Of The Ring Elf    Male     971
    ## 11 The Fellowship Of The Ring Hobbit Male    3644
    ## 12 The Fellowship Of The Ring Man    Male    1995
    ## 13 The Two Towers             Elf    Male     513
    ## 14 The Two Towers             Hobbit Male    2463
    ## 15 The Two Towers             Man    Male    3589
    ## 16 The Return Of The King     Elf    Male     510
    ## 17 The Return Of The King     Hobbit Male    2673
    ## 18 The Return Of The King     Man    Male    2459

``` r
unite(lotr_tidy, race_gender, Race, Gender)
```

    ## # A tibble: 18 x 3
    ##    Film                       race_gender   Words
    ##    <chr>                      <chr>         <int>
    ##  1 The Fellowship Of The Ring Elf_Female     1229
    ##  2 The Fellowship Of The Ring Hobbit_Female    14
    ##  3 The Fellowship Of The Ring Man_Female        0
    ##  4 The Two Towers             Elf_Female      331
    ##  5 The Two Towers             Hobbit_Female     0
    ##  6 The Two Towers             Man_Female      401
    ##  7 The Return Of The King     Elf_Female      183
    ##  8 The Return Of The King     Hobbit_Female     2
    ##  9 The Return Of The King     Man_Female      268
    ## 10 The Fellowship Of The Ring Elf_Male        971
    ## 11 The Fellowship Of The Ring Hobbit_Male    3644
    ## 12 The Fellowship Of The Ring Man_Male       1995
    ## 13 The Two Towers             Elf_Male        513
    ## 14 The Two Towers             Hobbit_Male    2463
    ## 15 The Two Towers             Man_Male       3589
    ## 16 The Return Of The King     Elf_Male        510
    ## 17 The Return Of The King     Hobbit_Male    2673
    ## 18 The Return Of The King     Man_Male       2459

``` r
mtcars
```

    ##                      mpg cyl  disp  hp drat    wt  qsec vs am gear carb
    ## Mazda RX4           21.0   6 160.0 110 3.90 2.620 16.46  0  1    4    4
    ## Mazda RX4 Wag       21.0   6 160.0 110 3.90 2.875 17.02  0  1    4    4
    ## Datsun 710          22.8   4 108.0  93 3.85 2.320 18.61  1  1    4    1
    ## Hornet 4 Drive      21.4   6 258.0 110 3.08 3.215 19.44  1  0    3    1
    ## Hornet Sportabout   18.7   8 360.0 175 3.15 3.440 17.02  0  0    3    2
    ## Valiant             18.1   6 225.0 105 2.76 3.460 20.22  1  0    3    1
    ## Duster 360          14.3   8 360.0 245 3.21 3.570 15.84  0  0    3    4
    ## Merc 240D           24.4   4 146.7  62 3.69 3.190 20.00  1  0    4    2
    ## Merc 230            22.8   4 140.8  95 3.92 3.150 22.90  1  0    4    2
    ## Merc 280            19.2   6 167.6 123 3.92 3.440 18.30  1  0    4    4
    ## Merc 280C           17.8   6 167.6 123 3.92 3.440 18.90  1  0    4    4
    ## Merc 450SE          16.4   8 275.8 180 3.07 4.070 17.40  0  0    3    3
    ## Merc 450SL          17.3   8 275.8 180 3.07 3.730 17.60  0  0    3    3
    ## Merc 450SLC         15.2   8 275.8 180 3.07 3.780 18.00  0  0    3    3
    ## Cadillac Fleetwood  10.4   8 472.0 205 2.93 5.250 17.98  0  0    3    4
    ## Lincoln Continental 10.4   8 460.0 215 3.00 5.424 17.82  0  0    3    4
    ## Chrysler Imperial   14.7   8 440.0 230 3.23 5.345 17.42  0  0    3    4
    ## Fiat 128            32.4   4  78.7  66 4.08 2.200 19.47  1  1    4    1
    ## Honda Civic         30.4   4  75.7  52 4.93 1.615 18.52  1  1    4    2
    ## Toyota Corolla      33.9   4  71.1  65 4.22 1.835 19.90  1  1    4    1
    ## Toyota Corona       21.5   4 120.1  97 3.70 2.465 20.01  1  0    3    1
    ## Dodge Challenger    15.5   8 318.0 150 2.76 3.520 16.87  0  0    3    2
    ## AMC Javelin         15.2   8 304.0 150 3.15 3.435 17.30  0  0    3    2
    ## Camaro Z28          13.3   8 350.0 245 3.73 3.840 15.41  0  0    3    4
    ## Pontiac Firebird    19.2   8 400.0 175 3.08 3.845 17.05  0  0    3    2
    ## Fiat X1-9           27.3   4  79.0  66 4.08 1.935 18.90  1  1    4    1
    ## Porsche 914-2       26.0   4 120.3  91 4.43 2.140 16.70  0  1    5    2
    ## Lotus Europa        30.4   4  95.1 113 3.77 1.513 16.90  1  1    5    2
    ## Ford Pantera L      15.8   8 351.0 264 4.22 3.170 14.50  0  1    5    4
    ## Ferrari Dino        19.7   6 145.0 175 3.62 2.770 15.50  0  1    5    6
    ## Maserati Bora       15.0   8 301.0 335 3.54 3.570 14.60  0  1    5    8
    ## Volvo 142E          21.4   4 121.0 109 4.11 2.780 18.60  1  1    4    2

``` r
expand(mtcars, vs, cyl)
```

    ## # A tibble: 6 x 2
    ##      vs   cyl
    ##   <dbl> <dbl>
    ## 1     0     4
    ## 2     0     6
    ## 3     0     8
    ## 4     1     4
    ## 5     1     6
    ## 6     1     8

``` r
expand(mtcars, nesting(vs,cyl))
```

    ## # A tibble: 5 x 2
    ##      vs   cyl
    ##   <dbl> <dbl>
    ## 1     0     4
    ## 2     0     6
    ## 3     0     8
    ## 4     1     4
    ## 5     1     6
