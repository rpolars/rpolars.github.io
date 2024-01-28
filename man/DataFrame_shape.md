

# Dimensions of a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/dataframe__frame.R#L429)

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
