
# Compute inverse hyperbolic cosine

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/#L)

## Description

Compute inverse hyperbolic cosine

## Usage

<pre><code class='language-R'>Expr_arccosh
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
