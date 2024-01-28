

# Product

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/after-wrappers.R#L20)

## Description

Compute the product of an expression.

## Usage

<pre><code class='language-R'>Expr_product()
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
