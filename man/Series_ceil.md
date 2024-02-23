

# Series_ceil

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/series__series.R#L590)

## Description

Ceil of this Series

## Usage

<pre><code class='language-R'>Series_ceil()
</code></pre>

## Value

bool

## Examples

``` r
library(polars)

pl$Series(c(.5, 1.999))$ceil()
```

    #> polars Series: shape: (2,)
    #> Series: '' [f64]
    #> [
    #>  1.0
    #>  2.0
    #> ]
