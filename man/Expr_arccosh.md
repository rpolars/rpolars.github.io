

# Compute inverse hyperbolic cosine

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/after-wrappers.R#L20)

## Description

Compute inverse hyperbolic cosine

## Usage

<pre><code class='language-R'>Expr_arccosh()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(-1, cosh(0.5), 0, 1, NA_real_))$
  with_columns(arccosh = pl$col("a")$arccosh())
```

    #> shape: (5, 2)
    #> ┌──────────┬─────────┐
    #> │ a        ┆ arccosh │
    #> │ ---      ┆ ---     │
    #> │ f64      ┆ f64     │
    #> ╞══════════╪═════════╡
    #> │ -1.0     ┆ NaN     │
    #> │ 1.127626 ┆ 0.5     │
    #> │ 0.0      ┆ NaN     │
    #> │ 1.0      ┆ 0.0     │
    #> │ null     ┆ null    │
    #> └──────────┴─────────┘
