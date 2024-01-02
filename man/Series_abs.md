
# Take absolute value of Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/series__series.R#L319)

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
