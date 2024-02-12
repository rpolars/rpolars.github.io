

# Compute inverse tangent

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/after-wrappers.R#L20)

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
