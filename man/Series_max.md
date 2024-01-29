

# max

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L653)

## Description

Reduce Series with max

## Usage

<pre><code class='language-R'>Series_max()
</code></pre>

## Details

The Dtypes Int8, UInt8, Int16 and UInt16 are cast to Int64 before
maxming to prevent overflow issues.

## Value

R scalar value

## Examples

``` r
library(polars)

pl$Series(c(1:2, NA, 3, 5))$max() # a NA is dropped always
```

    #> [1] 5

``` r
pl$Series(c(1:2, NA, 3, NaN, 4, Inf))$max() # NaN carries / poisons
```

    #> [1] Inf

``` r
pl$Series(c(1:2, 3, Inf, 4, -Inf, 5))$max() # Inf-Inf is NaN
```

    #> [1] Inf
