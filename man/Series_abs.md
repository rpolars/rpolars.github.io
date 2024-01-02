
# Take absolute value of Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/series__series.R#L319)

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
