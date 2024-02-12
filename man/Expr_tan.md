

# Compute tangent

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/after-wrappers.R#L20)

## Description

Compute tangent

## Usage

<pre><code class='language-R'>Expr_tan()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(0, pi / 2, pi, NA_real_))$
  with_columns(tangent = pl$col("a")$tan())
```

    #> shape: (4, 2)
    #> ┌──────────┬─────────────┐
    #> │ a        ┆ tangent     │
    #> │ ---      ┆ ---         │
    #> │ f64      ┆ f64         │
    #> ╞══════════╪═════════════╡
    #> │ 0.0      ┆ 0.0         │
    #> │ 1.570796 ┆ 1.6331e16   │
    #> │ 3.141593 ┆ -1.2246e-16 │
    #> │ null     ┆ null        │
    #> └──────────┴─────────────┘
