
# Series_floor

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/series__series.R#L401)

## Description

Floor of this Series

## Usage

<pre><code class='language-R'>Series_floor()
</code></pre>

## Value

numeric

## Examples

``` r
library(polars)

pl$Series(c(.5, 1.999))$floor()
```

    #> polars Series: shape: (2,)
    #> Series: '' [f64]
    #> [
    #>  0.0
    #>  1.0
    #> ]
