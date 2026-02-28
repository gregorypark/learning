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

“arrange” changes the order of rows

``` r
gapminder |> 
  arrange(desc(year))
```

    ## # A tibble: 1,704 × 6
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
    ## # ℹ 1,694 more rows

“distinct” finds unique rows

``` r
gapminder |> 
  distinct(continent)
```

    ## # A tibble: 5 × 1
    ##   continent
    ##   <fct>    
    ## 1 Asia     
    ## 2 Europe   
    ## 3 Africa   
    ## 4 Americas 
    ## 5 Oceania

``` r
gapminder |> 
  distinct(continent, year, .keep_all = TRUE)
```

    ## # A tibble: 60 × 6
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
    ## # ℹ 50 more rows

And “count” will provide row counts

``` r
gapminder |> 
  count(continent, sort = TRUE)
```

    ## # A tibble: 5 × 2
    ##   continent     n
    ##   <fct>     <int>
    ## 1 Africa      624
    ## 2 Asia        396
    ## 3 Europe      360
    ## 4 Americas    300
    ## 5 Oceania      24

## Columns

“mutate” adds columns based on existing ones

``` r
gapminder |> 
  mutate(pop_mil = pop / 1e6,
         .after = "pop"
         )
```

    ## # A tibble: 1,704 × 7
    ##    country     continent  year lifeExp      pop pop_mil gdpPercap
    ##    <fct>       <fct>     <int>   <dbl>    <int>   <dbl>     <dbl>
    ##  1 Afghanistan Asia       1952    28.8  8425333    8.43      779.
    ##  2 Afghanistan Asia       1957    30.3  9240934    9.24      821.
    ##  3 Afghanistan Asia       1962    32.0 10267083   10.3       853.
    ##  4 Afghanistan Asia       1967    34.0 11537966   11.5       836.
    ##  5 Afghanistan Asia       1972    36.1 13079460   13.1       740.
    ##  6 Afghanistan Asia       1977    38.4 14880372   14.9       786.
    ##  7 Afghanistan Asia       1982    39.9 12881816   12.9       978.
    ##  8 Afghanistan Asia       1987    40.8 13867957   13.9       852.
    ##  9 Afghanistan Asia       1992    41.7 16317921   16.3       649.
    ## 10 Afghanistan Asia       1997    41.8 22227415   22.2       635.
    ## # ℹ 1,694 more rows

“select” will provide a subset of columns

``` r
gapminder |> 
  select(!year:pop)
```

    ## # A tibble: 1,704 × 3
    ##    country     continent gdpPercap
    ##    <fct>       <fct>         <dbl>
    ##  1 Afghanistan Asia           779.
    ##  2 Afghanistan Asia           821.
    ##  3 Afghanistan Asia           853.
    ##  4 Afghanistan Asia           836.
    ##  5 Afghanistan Asia           740.
    ##  6 Afghanistan Asia           786.
    ##  7 Afghanistan Asia           978.
    ##  8 Afghanistan Asia           852.
    ##  9 Afghanistan Asia           649.
    ## 10 Afghanistan Asia           635.
    ## # ℹ 1,694 more rows

``` r
gapminder |> 
  mutate(pop_mil = pop / 1e6) |> 
  select(contains("pop"))
```

    ## # A tibble: 1,704 × 2
    ##         pop pop_mil
    ##       <int>   <dbl>
    ##  1  8425333    8.43
    ##  2  9240934    9.24
    ##  3 10267083   10.3 
    ##  4 11537966   11.5 
    ##  5 13079460   13.1 
    ##  6 14880372   14.9 
    ##  7 12881816   12.9 
    ##  8 13867957   13.9 
    ##  9 16317921   16.3 
    ## 10 22227415   22.2 
    ## # ℹ 1,694 more rows

“rename” put the new name on the left

``` r
gapminder |> 
  rename(population = pop)
```

    ## # A tibble: 1,704 × 6
    ##    country     continent  year lifeExp population gdpPercap
    ##    <fct>       <fct>     <int>   <dbl>      <int>     <dbl>
    ##  1 Afghanistan Asia       1952    28.8    8425333      779.
    ##  2 Afghanistan Asia       1957    30.3    9240934      821.
    ##  3 Afghanistan Asia       1962    32.0   10267083      853.
    ##  4 Afghanistan Asia       1967    34.0   11537966      836.
    ##  5 Afghanistan Asia       1972    36.1   13079460      740.
    ##  6 Afghanistan Asia       1977    38.4   14880372      786.
    ##  7 Afghanistan Asia       1982    39.9   12881816      978.
    ##  8 Afghanistan Asia       1987    40.8   13867957      852.
    ##  9 Afghanistan Asia       1992    41.7   16317921      649.
    ## 10 Afghanistan Asia       1997    41.8   22227415      635.
    ## # ℹ 1,694 more rows
