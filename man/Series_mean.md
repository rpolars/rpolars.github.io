
# Mean

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/series__series.R#L615)

## Description

Reduce Series with mean

## Usage

<pre><code class='language-R'>Series_mean()
</code></pre>

## Details

The Dtypes Int8, UInt8, Int16 and UInt16 are cast to Int64 before
meanming to prevent overflow issues.

## Value

R scalar value

## Examples

``` r
library(polars)

pl$Series(c(1:2, NA, 3, 5))$mean() # a NA is dropped always
```

    #> [1] 2.75

``` r
pl$Series(c(1:2, NA, 3, NaN, 4, Inf))$mean() # NaN carries / poisons
```

    #> [1] NaN

``` r
pl$Series(c(1:2, 3, Inf, 4, -Inf, 5))$mean() # Inf-Inf is NaN
```

    #> [1] NaN
