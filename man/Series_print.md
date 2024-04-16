

# Print Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/series__series.R#L359)

## Description

Print Series

## Usage

<pre><code class='language-R'>Series_print()
</code></pre>

## Value

self

## Examples

``` r
library(polars)

as_polars_series(1:3)
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #> ]
