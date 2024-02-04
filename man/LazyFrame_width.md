

# Number of columns of a LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/lazyframe__lazy.R#L1396)

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
