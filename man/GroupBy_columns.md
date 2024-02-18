

# Get and set column names of a GroupBy

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/group_by.R#L86)

## Description

Get and set column names of a GroupBy

## Usage

<pre><code class='language-R'>GroupBy_columns()
</code></pre>

## Value

A character vector with the column names.

## Examples

``` r
library(polars)

gb = pl$DataFrame(iris)$group_by("Species")

# get values
gb$columns
```

    #> [1] "Sepal.Length" "Sepal.Width"  "Petal.Length" "Petal.Width"  "Species"
