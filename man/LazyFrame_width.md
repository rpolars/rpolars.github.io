

# Number of columns of a LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/lazyframe__lazy.R#L1396)

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
