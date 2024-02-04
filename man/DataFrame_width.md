

# Number of columns of a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/dataframe__frame.R#L457)

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
