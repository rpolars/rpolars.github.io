
# Compute the exponential of the elements

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/#L)

## Description

Compute the exponential of the elements

## Usage

<pre><code class='language-R'>Expr_exp
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
