

# Find the max of a Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L766)

## Description

Find the max of a Series

## Usage

<pre><code class='language-R'>Series_max()
</code></pre>

## Details

The Dtypes Int8, UInt8, Int16 and UInt16 are cast to Int64 before
summing to prevent overflow issues.

## Value

A numeric value

## Examples

``` r
library(polars)

as_polars_series(c(1:2, NA, 3, 5))$max() # a NA is dropped always
```

    #> [1] 5

``` r
as_polars_series(c(1:2, NA, 3, NaN, 4, Inf))$max() # NaN carries / poisons
```

    #> [1] Inf

``` r
as_polars_series(c(1:2, 3, Inf, 4, -Inf, 5))$max() # Inf-Inf is NaN
```

    #> [1] Inf
