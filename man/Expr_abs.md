

# Compute the absolute values

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/after-wrappers.R#L20)

## Description

Compute the absolute values

## Usage

<pre><code class='language-R'>Expr_abs()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = -1:1)$
  with_columns(abs = pl$col("a")$abs())
```

    #> shape: (3, 2)
    #> ┌─────┬─────┐
    #> │ a   ┆ abs │
    #> │ --- ┆ --- │
    #> │ i32 ┆ i32 │
    #> ╞═════╪═════╡
    #> │ -1  ┆ 1   │
    #> │ 0   ┆ 0   │
    #> │ 1   ┆ 1   │
    #> └─────┴─────┘
