
# Compute inverse sine

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/after-wrappers.R#L20)

## Description

Compute inverse sine

## Usage

<pre><code class='language-R'>Expr_arcsin()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(-1, sin(0.5), 0, 1, NA_real_))$
  with_columns(arcsin = pl$col("a")$arcsin())
```

    #> shape: (5, 2)
    #> ┌──────────┬───────────┐
    #> │ a        ┆ arcsin    │
    #> │ ---      ┆ ---       │
    #> │ f64      ┆ f64       │
    #> ╞══════════╪═══════════╡
    #> │ -1.0     ┆ -1.570796 │
    #> │ 0.479426 ┆ 0.5       │
    #> │ 0.0      ┆ 0.0       │
    #> │ 1.0      ┆ 1.570796  │
    #> │ null     ┆ null      │
    #> └──────────┴───────────┘
