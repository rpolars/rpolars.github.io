

# Take absolute value of Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/series__series.R#L320)

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
