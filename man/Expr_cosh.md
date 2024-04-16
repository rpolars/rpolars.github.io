

# Compute hyperbolic cosine

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/after-wrappers.R#L20)

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

pl$DataFrame(a = c(-1, acosh(2), 0, 1, NA_real_))$
  with_columns(cosh = pl$col("a")$cosh())
```

    #> shape: (5, 2)
    #> ┌──────────┬──────────┐
    #> │ a        ┆ cosh     │
    #> │ ---      ┆ ---      │
    #> │ f64      ┆ f64      │
    #> ╞══════════╪══════════╡
    #> │ -1.0     ┆ 1.543081 │
    #> │ 1.316958 ┆ 2.0      │
    #> │ 0.0      ┆ 1.0      │
    #> │ 1.0      ┆ 1.543081 │
    #> │ null     ┆ null     │
    #> └──────────┴──────────┘
