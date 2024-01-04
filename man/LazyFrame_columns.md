
# Get the column names of a LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/lazyframe__lazy.R#L1274)

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
