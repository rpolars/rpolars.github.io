
# Number of columns of a LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/lazyframe__lazy.R#L1288)

## Description

Get the number of columns (width) of a LazyFrame

## Usage

<pre><code class='language-R'>LazyFrame_width()
</code></pre>

## Value

The number of columns of a DataFrame

## Examples

``` r
library(polars)

pl$LazyFrame(mtcars)$width
```

    #> [1] 11
