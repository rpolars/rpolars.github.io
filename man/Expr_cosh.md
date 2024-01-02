
# Compute hyperbolic cosine

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/#L)

## Description

Compute hyperbolic cosine

## Usage

<pre><code class='language-R'>Expr_cosh
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
