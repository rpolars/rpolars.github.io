
# Get data type of Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/series__series.R#L692)

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
