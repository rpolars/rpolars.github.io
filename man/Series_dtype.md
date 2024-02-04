

# Get data type of Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/series__series.R#L701)

## Description

Get data type of Series

## Usage

<pre><code class='language-R'>Series_dtype()
</code></pre>

## Value

DataType

## Examples

``` r
library(polars)

pl$Series(1:4)$dtype
```

    #> DataType: Int32

``` r
pl$Series(c(1, 2))$dtype
```

    #> DataType: Float64

``` r
pl$Series(letters)$dtype
```

    #> DataType: String
