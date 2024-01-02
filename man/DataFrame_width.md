
# Number of columns of a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/dataframe__frame.R#L451)

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
