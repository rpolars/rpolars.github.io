

# Compute sine

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/after-wrappers.R#L20)

## Description

Compute sine

## Usage

<pre><code class='language-R'>Expr_sin()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(0, pi / 2, pi, NA_real_))$
  with_columns(sine = pl$col("a")$sin())
```

    #> shape: (4, 2)
    #> ┌──────────┬────────────┐
    #> │ a        ┆ sine       │
    #> │ ---      ┆ ---        │
    #> │ f64      ┆ f64        │
    #> ╞══════════╪════════════╡
    #> │ 0.0      ┆ 0.0        │
    #> │ 1.570796 ┆ 1.0        │
    #> │ 3.141593 ┆ 1.2246e-16 │
    #> │ null     ┆ null       │
    #> └──────────┴────────────┘
