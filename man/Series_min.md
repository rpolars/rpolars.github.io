

# min

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L814)

## Description

Reduce Series with min

## Usage

<pre><code class='language-R'>Series_min()
</code></pre>

## Details

The Dtypes Int8, UInt8, Int16 and UInt16 are cast to Int64 before taking
the min to prevent overflow issues.

## Value

R scalar value

## Examples

``` r
library(polars)

pl$Series(c(1:2, NA, 3, 5))$min() # a NA is dropped always
```

    #> [1] 1

``` r
pl$Series(c(1:2, NA, 3, NaN, 4, Inf))$min() # NaN carries / poisons
```

    #> [1] 1

``` r
pl$Series(c(1:2, 3, Inf, 4, -Inf, 5))$min() # Inf-Inf is NaN
```

    #> [1] -Inf
