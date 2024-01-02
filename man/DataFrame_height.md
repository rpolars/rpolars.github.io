
# Number of rows of a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/dataframe__frame.R#L438)

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
