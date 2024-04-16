

# Compute inverse tangent

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/after-wrappers.R#L20)

## Description

Compute inverse tangent

## Usage

<pre><code class='language-R'>Expr_arctan()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(-1, tan(0.5), 0, 1, NA_real_))$
  with_columns(arctan = pl$col("a")$arctan())
```

    #> shape: (5, 2)
    #> ┌──────────┬───────────┐
    #> │ a        ┆ arctan    │
    #> │ ---      ┆ ---       │
    #> │ f64      ┆ f64       │
    #> ╞══════════╪═══════════╡
    #> │ -1.0     ┆ -0.785398 │
    #> │ 0.546302 ┆ 0.5       │
    #> │ 0.0      ┆ 0.0       │
    #> │ 1.0      ┆ 0.785398  │
    #> │ null     ┆ null      │
    #> └──────────┴───────────┘
