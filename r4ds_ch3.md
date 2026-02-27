r4ds applications
================
Gregory Park
2026-02-27

## Loading

I will be working with “gapminder” dataset, which features country,
continent, year, life expectancy, population, and gdp per capita

``` r
library(tidyverse); library(gapminder)

view(gapminder)
gapminder 
```

    ## # A tibble: 1,704 × 6
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
    ## # ℹ 1,694 more rows

``` r
?gapminder
```

## Row work

“filter” if you want specific rows based on column rules

``` r
gapminder |> 
  filter(year > 1990)
```

    ## # A tibble: 568 × 6
    ##    country     continent  year lifeExp      pop gdpPercap
    ##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
    ##  1 Afghanistan Asia       1992    41.7 16317921      649.
    ##  2 Afghanistan Asia       1997    41.8 22227415      635.
    ##  3 Afghanistan Asia       2002    42.1 25268405      727.
    ##  4 Afghanistan Asia       2007    43.8 31889923      975.
    ##  5 Albania     Europe     1992    71.6  3326498     2497.
    ##  6 Albania     Europe     1997    73.0  3428038     3193.
    ##  7 Albania     Europe     2002    75.7  3508512     4604.
    ##  8 Albania     Europe     2007    76.4  3600523     5937.
    ##  9 Algeria     Africa     1992    67.7 26298373     5023.
    ## 10 Algeria     Africa     1997    69.2 29072015     4797.
    ## # ℹ 558 more rows

``` r
gapminder |> 
  filter(continent == "Asia" | continent == "Europe")
```

    ## # A tibble: 756 × 6
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
    ## # ℹ 746 more rows

``` r
# combines | and & functions
gapminder |> 
  filter(country %in% c("Afghanistan","Albania"))
```

    ## # A tibble: 24 × 6
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
    ## # ℹ 14 more rows

``` r
# dplyr functions never modify their inputs
new <- gapminder |> 
  filter(year == 2007)
view(new)
```
