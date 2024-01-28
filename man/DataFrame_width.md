

# Number of columns of a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/dataframe__frame.R#L457)

## Description

Get the number of columns (width) of a DataFrame

## Usage

<pre><code class='language-R'>DataFrame_width()
</code></pre>

## Value

The number of columns of a DataFrame

## Examples

``` r
library(polars)

pl$DataFrame(iris)$width
```

    #> [1] 5
