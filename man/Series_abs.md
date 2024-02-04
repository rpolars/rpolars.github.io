

# Take absolute value of Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/series__series.R#L320)

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
