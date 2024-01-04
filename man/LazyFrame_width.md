
# Number of columns of a LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/lazyframe__lazy.R#L1288)

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
