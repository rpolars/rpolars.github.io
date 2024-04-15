

# Compute the mean of a Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/series__series.R#L804)

## Description

Compute the mean of a Series

## Usage

<pre><code class='language-R'>Series_mean()
</code></pre>

## Details

The Dtypes Int8, UInt8, Int16 and UInt16 are cast to Int64 before
summing to prevent overflow issues.

## Value

A numeric value

## Examples

``` r
library(polars)

as_polars_series(c(1:2, NA, 3, 5))$mean() # a NA is dropped always
```

    #> [1] 2.75

``` r
as_polars_series(c(1:2, NA, 3, NaN, 4, Inf))$mean() # NaN carries / poisons
```

    #> [1] NaN

``` r
as_polars_series(c(1:2, 3, Inf, 4, -Inf, 5))$mean() # Inf-Inf is NaN
```

    #> [1] NaN
