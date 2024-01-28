

# Get data type of Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/series__series.R#L686)

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
