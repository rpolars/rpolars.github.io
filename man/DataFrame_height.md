

# Number of rows of a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/dataframe__frame.R#L444)

## Description

Get the number of rows (height) of a DataFrame

## Usage

<pre><code class='language-R'>DataFrame_height()
</code></pre>

## Value

The number of rows of the DataFrame

## Examples

``` r
library(polars)

pl$DataFrame(iris)$height
```

    #> [1] 150
