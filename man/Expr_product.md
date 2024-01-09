
# Product

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/#L)

## Description

Compute the product of an expression.

## Usage

<pre><code class='language-R'>Expr_product
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(x = c(2L, NA, 2L))$
  with_columns(product = pl$col("x")$product())
```

    #> shape: (3, 2)
    #> ┌──────┬─────────┐
    #> │ x    ┆ product │
    #> │ ---  ┆ ---     │
    #> │ i32  ┆ i64     │
    #> ╞══════╪═════════╡
    #> │ 2    ┆ 4       │
    #> │ null ┆ 4       │
    #> │ 2    ┆ 4       │
    #> └──────┴─────────┘
