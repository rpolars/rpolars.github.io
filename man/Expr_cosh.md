

# Compute hyperbolic cosine

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/after-wrappers.R#L20)

## Description

Compute hyperbolic cosine

## Usage

<pre><code class='language-R'>Expr_cosh()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(-1, acosh(0.5), 0, 1, NA_real_))$
  with_columns(cosh = pl$col("a")$cosh())
```

    #> shape: (5, 2)
    #> ┌──────┬──────────┐
    #> │ a    ┆ cosh     │
    #> │ ---  ┆ ---      │
    #> │ f64  ┆ f64      │
    #> ╞══════╪══════════╡
    #> │ -1.0 ┆ 1.543081 │
    #> │ NaN  ┆ NaN      │
    #> │ 0.0  ┆ 1.0      │
    #> │ 1.0  ┆ 1.543081 │
    #> │ null ┆ null     │
    #> └──────┴──────────┘
