

# Compute inverse hyperbolic sine

[**Source code**](https://github.com/pola-rs/r-polars/tree/mkdocs-matrial-search-preview/R/after-wrappers.R#L20)

## Description

Compute inverse hyperbolic sine

## Usage

<pre><code class='language-R'>Expr_arcsinh()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(-1, sinh(0.5), 0, 1, NA_real_))$
  with_columns(arcsinh = pl$col("a")$arcsinh())
```

    #> shape: (5, 2)
    #> ┌──────────┬───────────┐
    #> │ a        ┆ arcsinh   │
    #> │ ---      ┆ ---       │
    #> │ f64      ┆ f64       │
    #> ╞══════════╪═══════════╡
    #> │ -1.0     ┆ -0.881374 │
    #> │ 0.521095 ┆ 0.5       │
    #> │ 0.0      ┆ 0.0       │
    #> │ 1.0      ┆ 0.881374  │
    #> │ null     ┆ null      │
    #> └──────────┴───────────┘
