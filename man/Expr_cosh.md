

# Compute hyperbolic cosine

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/after-wrappers.R#L20)

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
