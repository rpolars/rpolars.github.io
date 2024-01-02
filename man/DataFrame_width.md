
# Number of columns of a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/dataframe__frame.R#L451)

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
