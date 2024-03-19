

# Compute the sum of a Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L720)

## Description

Compute the sum of a Series

## Usage

<pre><code class='language-R'>Series_sum()
</code></pre>

## Details

The Dtypes Int8, UInt8, Int16 and UInt16 are cast to Int64 before
summing to prevent overflow issues.

## Value

A numeric value

## Examples

``` r
library(polars)

pl$Series(c(1:2, NA, 3, 5))$sum() # a NA is dropped always
```

    #> [1] 11

``` r
pl$Series(c(1:2, NA, 3, NaN, 4, Inf))$sum() # NaN poisons the result
```

    #> [1] NaN

``` r
pl$Series(c(1:2, 3, Inf, 4, -Inf, 5))$sum() # Inf-Inf is NaN
```

    #> [1] NaN
