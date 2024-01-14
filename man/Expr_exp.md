
# Compute the exponential of the elements

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/after-wrappers.R#L20)

## Description

Compute the exponential of the elements

## Usage

<pre><code class='language-R'>Expr_exp()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = -1:3)$with_columns(a_exp = pl$col("a")$exp())
```

    #> shape: (5, 2)
    #> ┌─────┬───────────┐
    #> │ a   ┆ a_exp     │
    #> │ --- ┆ ---       │
    #> │ i32 ┆ f64       │
    #> ╞═════╪═══════════╡
    #> │ -1  ┆ 0.367879  │
    #> │ 0   ┆ 1.0       │
    #> │ 1   ┆ 2.718282  │
    #> │ 2   ┆ 7.389056  │
    #> │ 3   ┆ 20.085537 │
    #> └─────┴───────────┘
