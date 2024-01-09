
# Dimensions of a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/dataframe__frame.R#L423)

## Description

Get shape/dimensions of DataFrame

## Usage

<pre><code class='language-R'>DataFrame_shape()
</code></pre>

## Value

Numeric vector of length two with the number of rows and the number of
columns.

## Examples

``` r
library(polars)

pl$DataFrame(iris)$shape
```

    #> [1] 150   5
