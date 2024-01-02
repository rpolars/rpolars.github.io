
# Series_floor

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/series__series.R#L402)

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
