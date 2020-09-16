p8105\_homework1\_xl2834
================
Xiaoyu Li
9/15/2020

``` r
library(tidyverse)
```

    ## -- Attaching packages -------------------------------- tidyverse 1.3.0 --

    ## v ggplot2 3.3.2     v purrr   0.3.4
    ## v tibble  3.0.3     v dplyr   1.0.2
    ## v tidyr   1.1.2     v stringr 1.4.0
    ## v readr   1.3.1     v forcats 0.5.0

    ## -- Conflicts ----------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

## Problem 1

Create a data frame with the specified elements.

``` r
prob1_df = 
  tibble(
    samp = rnorm(10),
    vec_logical = samp > 0,
    vec_char = c("a", "b", "c", "d", "e", "f", "g", "h", "i", "j" ),
    vec_factor = factor(c("low", "mod", "low", "mod", "high", "low",                           "mod", "high", "high", "low"))
)
```

Take the mean of the variables in the data frame.

``` r
mean(pull(prob1_df, samp))
```

    ## [1] 0.2278455

``` r
mean(pull(prob1_df, vec_logical))
```

    ## [1] 0.7

``` r
mean(pull(prob1_df, vec_char))
```

    ## Warning in mean.default(pull(prob1_df, vec_char)): argument is not numeric or
    ## logical: returning NA

    ## [1] NA

``` r
mean(pull(prob1_df, vec_factor))
```

    ## Warning in mean.default(pull(prob1_df, vec_factor)): argument is not numeric or
    ## logical: returning NA

    ## [1] NA

I can take the mean of numeric sample and logical vector, but not the
character and factor.

Convert the logical vector to other types.

``` r
as.numeric(pull(prob1_df,vec_logical)) * pull(prob1_df, samp)
as.factor(pull(prob1_df,vec_logical)) * pull(prob1_df, samp)
as.numeric(as.factor(pull(prob1_df,vec_logical))) * pull(prob1_df, samp)
```

I can multiply the numeric sample with the logical vector after it was
converted to numeric or converted to factor and then numeric, but not
after it was converted to a factor.

This can help to explain why I cannot take the mean of a factor (because
the operators like “+” and "\*" are not meaningful for factors).

## Problem 2

Download the package containing the penguins dataset.

``` r
data("penguins", package = "palmerpenguins")
```

This dataset include variables bill\_depth\_mm, bill\_length\_mm,
body\_mass\_g, flipper\_length\_mm, island, sex, species, year. The size
of the dataset is 344 \* 8. The mean flipper length is NA.

#### Plot

Make a scatterplot.

``` r
ggplot(penguins, aes(x = bill_length_mm, y = flipper_length_mm, color = species)) + geom_point()
```

    ## Warning: Removed 2 rows containing missing values (geom_point).

![](p8105_homework1_xl2834_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

Save the plot.

``` r
ggsave("scatterplot.pdf")
```

    ## Saving 7 x 5 in image

    ## Warning: Removed 2 rows containing missing values (geom_point).
