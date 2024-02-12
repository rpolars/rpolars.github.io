

# Number of columns of a LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/lazyframe__lazy.R#L1413)

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
