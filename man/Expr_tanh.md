

# Compute hyperbolic tangent

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/after-wrappers.R#L20)

## Description

Compute hyperbolic tangent

## Usage

<pre><code class='language-R'>Expr_tanh()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(-1, atanh(0.5), 0, 1, NA_real_))$
  with_columns(tanh = pl$col("a")$tanh())
```

    #> shape: (5, 2)
    #> ┌──────────┬───────────┐
    #> │ a        ┆ tanh      │
    #> │ ---      ┆ ---       │
    #> │ f64      ┆ f64       │
    #> ╞══════════╪═══════════╡
    #> │ -1.0     ┆ -0.761594 │
    #> │ 0.549306 ┆ 0.5       │
    #> │ 0.0      ┆ 0.0       │
    #> │ 1.0      ┆ 0.761594  │
    #> │ null     ┆ null      │
    #> └──────────┴───────────┘
