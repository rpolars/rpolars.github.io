

# Get sum value

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/after-wrappers.R#L20)

## Description

Get sum value

## Usage

<pre><code class='language-R'>Expr_sum()
</code></pre>

## Details

The dtypes Int8, UInt8, Int16 and UInt16 are cast to Int64 before
summing to prevent overflow issues.

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(x = c(1L, NA, 2L))$
  with_columns(sum = pl$col("x")$sum())
```

    #> shape: (3, 2)
    #> ┌──────┬─────┐
    #> │ x    ┆ sum │
    #> │ ---  ┆ --- │
    #> │ i32  ┆ i32 │
    #> ╞══════╪═════╡
    #> │ 1    ┆ 3   │
    #> │ null ┆ 3   │
    #> │ 2    ┆ 3   │
    #> └──────┴─────┘
