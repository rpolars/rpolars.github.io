
# Series_floor

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/series__series.R#L402)

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
