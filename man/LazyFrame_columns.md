
# Get the column names of a LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/lazyframe__lazy.R#L1274)

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
