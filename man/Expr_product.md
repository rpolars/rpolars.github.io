

# Product

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/after-wrappers.R#L20)

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
