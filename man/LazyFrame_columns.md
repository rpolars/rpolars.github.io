

# Get the column names of a LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/lazyframe__lazy.R#L1399)

## Description

Get the column names of a LazyFrame

## Usage

<pre><code class='language-R'>LazyFrame_columns()
</code></pre>

## Value

A vector of column names

## Examples

``` r
library(polars)

pl$LazyFrame(mtcars)$columns
```

    #>  [1] "mpg"  "cyl"  "disp" "hp"   "drat" "wt"   "qsec" "vs"   "am"   "gear"
    #> [11] "carb"
