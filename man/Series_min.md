

# Find the min of a Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/series__series.R#L837)

## Description

Find the min of a Series

## Usage

<pre><code class='language-R'>Series_min()
</code></pre>

## Details

The Dtypes Int8, UInt8, Int16 and UInt16 are cast to Int64 before
summing to prevent overflow issues.

## Value

A numeric value

## Examples

``` r
library(polars)

as_polars_series(c(1:2, NA, 3, 5))$min() # a NA is dropped always
```

    #> [1] 1

``` r
as_polars_series(c(1:2, NA, 3, NaN, 4, Inf))$min() # NaN carries / poisons
```

    #> [1] 1

``` r
as_polars_series(c(1:2, 3, Inf, 4, -Inf, 5))$min() # Inf-Inf is NaN
```

    #> [1] -Inf
