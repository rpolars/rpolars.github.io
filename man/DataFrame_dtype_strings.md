

# Data types information

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/after-wrappers.R#L20)

## Description

Get the data type of all columns as strings. You can see all available
types with <code>names(pl$dtypes)</code>. The data type of each column
is also shown when printing the DataFrame.

## Usage

<pre><code class='language-R'>DataFrame_dtype_strings()
</code></pre>

## Value

A character vector with the data type of each column

## Examples

``` r
library(polars)

pl$DataFrame(iris)$dtype_strings()
```

    #> [1] "f64" "f64" "f64" "f64" "cat"
