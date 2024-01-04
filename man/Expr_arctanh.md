
# Compute inverse hyperbolic tangent

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/#L)

## Description

Compute inverse hyperbolic tangent

## Usage

<pre><code class='language-R'>Expr_arctanh
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(-1, tanh(0.5), 0, 1, NA_real_))$
  with_columns(arctanh = pl$col("a")$arctanh())
```

    #> shape: (5, 2)
    #> ┌──────────┬─────────┐
    #> │ a        ┆ arctanh │
    #> │ ---      ┆ ---     │
    #> │ f64      ┆ f64     │
    #> ╞══════════╪═════════╡
    #> │ -1.0     ┆ -inf    │
    #> │ 0.462117 ┆ 0.5     │
    #> │ 0.0      ┆ 0.0     │
    #> │ 1.0      ┆ inf     │
    #> │ null     ┆ null    │
    #> └──────────┴─────────┘
