

# Compute the median of a Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L815)

## Description

Compute the median of a Series

## Usage

<pre><code class='language-R'>Series_median()
</code></pre>

## Details

The Dtypes Int8, UInt8, Int16 and UInt16 are cast to Int64 before
summing to prevent overflow issues.

## Value

A numeric value

## Examples

``` r
library(polars)

as_polars_series(c(1:2, NA, 3, 5))$median() # a NA is dropped always
```

    #> [1] 2.5

``` r
as_polars_series(c(1:2, NA, 3, NaN, 4, Inf))$median() # NaN carries / poisons
```

    #> [1] 3.5

``` r
as_polars_series(c(1:2, 3, Inf, 4, -Inf, 5))$median() # Inf-Inf is NaN
```

    #> [1] 3
