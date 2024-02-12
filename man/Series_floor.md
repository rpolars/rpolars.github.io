

# Series_floor

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/series__series.R#L395)

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
