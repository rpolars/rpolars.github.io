

# Get and set column names of a LazyGroupBy

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__group_by.R#L48)

## Description

Get and set column names of a LazyGroupBy

## Usage

<pre><code class='language-R'>LazyGroupBy_columns()
</code></pre>

## Value

A character vector with the column names.

## Examples

``` r
library(polars)

lgb = pl$LazyFrame(iris)$group_by("Species")

# get values
lgb$columns
```

    #> [1] "Sepal.Length" "Sepal.Width"  "Petal.Length" "Petal.Width"  "Species"
