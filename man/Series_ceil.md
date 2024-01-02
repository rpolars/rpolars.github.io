
# Series_ceil

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/series__series.R#L417)

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
