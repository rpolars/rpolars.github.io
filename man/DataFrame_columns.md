

# Get and set column names of a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L342)

## Description

Get and set column names of a DataFrame

## Usage

<pre><code class='language-R'>DataFrame_columns()
</code></pre>

## Value

A character vector with the column names.

## Examples

``` r
library(polars)

df = pl$DataFrame(iris)

# get values
df$columns
```

    #> [1] "Sepal.Length" "Sepal.Width"  "Petal.Length" "Petal.Width"  "Species"

``` r
# set + get values
df$columns = letters[1:5] # <- is fine too
df$columns
```

    #> [1] "a" "b" "c" "d" "e"
