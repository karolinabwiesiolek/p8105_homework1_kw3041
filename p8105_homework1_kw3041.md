p8105_homework1_kw3041
================
2025-09-20

Here, I will run a code to display the first 6 rows of the dataset in
order to access the data.

``` r
library(moderndive)
library(ggplot2)
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.2
    ## ✔ lubridate 1.9.4     ✔ tibble    3.3.0
    ## ✔ purrr     1.1.0     ✔ tidyr     1.3.1
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
data("early_january_weather")
head(early_january_weather)
```

    ## # A tibble: 6 × 15
    ##   origin  year month   day  hour  temp  dewp humid wind_dir wind_speed wind_gust
    ##   <chr>  <int> <int> <int> <int> <dbl> <dbl> <dbl>    <dbl>      <dbl>     <dbl>
    ## 1 EWR     2013     1     1     1  39.0  26.1  59.4      270      10.4         NA
    ## 2 EWR     2013     1     1     2  39.0  27.0  61.6      250       8.06        NA
    ## 3 EWR     2013     1     1     3  39.0  28.0  64.4      240      11.5         NA
    ## 4 EWR     2013     1     1     4  39.9  28.0  62.2      250      12.7         NA
    ## 5 EWR     2013     1     1     5  39.0  28.0  64.4      260      12.7         NA
    ## 6 EWR     2013     1     1     6  37.9  28.0  67.2      240      11.5         NA
    ## # ℹ 4 more variables: precip <dbl>, pressure <dbl>, visib <dbl>,
    ## #   time_hour <dttm>

## Short description of this data set!

This data includes variables such as `temp`, which is measured in
Fahrenheit, and `dewp`, which is a measure of dewpoint; `humid` for
relative humidity; `wind_speed`, and a few more variables.

## Checking the structure of early_january_weather tibble:

The early_january_weather dataset contains following number of rows:

``` r
nrow(early_january_weather)
```

    ## [1] 358

The early_january_weather dataset contains the following numner of
columns:

``` r
ncol(early_january_weather)
```

    ## [1] 15

The mean temperature of this dataset is:

``` r
mean(early_january_weather[["temp"]], na.rm = TRUE)
```

    ## [1] 39.58212

## Plot of the Weather

``` r
weather_plot <- ggplot2::ggplot(
  early_january_weather,
  ggplot2::aes(x = time_hour, y = temp, color = humid)
) +
  ggplot2::geom_point(alpha = 0.5) + 
  ggplot2::labs(
    title = "Temperature over Time; Colored by Humidity",
    x = "Time (hour)",
    y = "Temperature (F)",
    color = "Humidity"
  ) + 
    ggplot2::theme_minimal()

weather_plot
```

![](p8105_homework1_kw3041_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

``` r
ggplot2::ggsave("scatterplot_weather12.png", plot = weather_plot, width = 7, height = 4)
```

## Problem 2. Here, first I will set a random numeric sample.

``` r
set.seed(123) 
numeric_vec = rnorm(10)
```

``` r
logical_vec = numeric_vec > 0
```

``` r
char_vec = letters[1:10]
```

``` r
factor_vec = factor(sample(c("Low", "Medium", "High"), size = 10, replace = TRUE ))
```

``` r
df = data.frame(
  numeric_var = numeric_vec,
  logical_var = logical_vec,
  char_var = char_vec,
  factor_var = factor_vec
)

df
```

    ##    numeric_var logical_var char_var factor_var
    ## 1  -0.56047565       FALSE        a        Low
    ## 2  -0.23017749       FALSE        b        Low
    ## 3   1.55870831        TRUE        c        Low
    ## 4   0.07050839        TRUE        d        Low
    ## 5   0.12928774        TRUE        e       High
    ## 6   1.71506499        TRUE        f     Medium
    ## 7   0.46091621        TRUE        g       High
    ## 8  -1.26506123       FALSE        h     Medium
    ## 9  -0.68685285       FALSE        i        Low
    ## 10 -0.44566197       FALSE        j     Medium

Taking mean from each variable

\#Numeric and logical mean

``` r
mean(df[ , "numeric_var"])
```

    ## [1] 0.07462564

``` r
mean(df[, "logical_var"])
```

    ## [1] 0.5

``` r
mean(df[ , "char_var"])
```

    ## Warning in mean.default(df[, "char_var"]): argument is not numeric or logical:
    ## returning NA

    ## [1] NA

``` r
mean(df[ , "factor_var"])
```

    ## Warning in mean.default(df[, "factor_var"]): argument is not numeric or
    ## logical: returning NA

    ## [1] NA

Only numeric and logical variables can be avergaed directly, if we
wanted to get the avergae of facotrs and characters we would first need
to convert or assign them a numeric conversion.
