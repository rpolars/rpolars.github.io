
# Compute the absolute values

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/#L)

## Description

Compute the absolute values

## Usage

<pre><code class='language-R'>Expr_abs
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
