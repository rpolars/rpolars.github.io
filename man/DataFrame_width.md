

# Number of columns of a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/dataframe__frame.R#L463)

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
