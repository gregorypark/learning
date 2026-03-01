styling code properly
================
Gregory Park
2026-03-01

command + shift + p is a useful shortcut

``` r
library(styler); library(tidyverse); library(nycflights13)
```

variable names: lowercase, underscores, descriptive \> short

make operations well spaced out

``` r
# Strive for
z <- (1 + 2)^2 / 4

# Avoid
z<-( 1 + 2 ) ^ 2/4
```

new arguments on new lines

``` r
# Strive for
flights |>  
  group_by(tailnum) |> 
  summarize(
    delay = mean(arr_delay, na.rm = TRUE),
    n = n()
  )

# Avoid
flights |>
  group_by(
    tailnum
  ) |> 
  summarize(delay = mean(arr_delay, na.rm = TRUE), n = n())
```
