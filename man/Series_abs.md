

# Take absolute value of Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L478)

## Description

Take absolute value of Series

## Usage

<pre><code class='language-R'>Series_abs()
</code></pre>

## Value

Series

## Examples

``` r
library(polars)

pl$Series(-2:2)$abs()
```

    #> polars Series: shape: (5,)
    #> Series: '' [i32]
    #> [
    #>  2
    #>  1
    #>  0
    #>  1
    #>  2
    #> ]
