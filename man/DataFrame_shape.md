

# Dimensions of a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/dataframe__frame.R#L435)

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
