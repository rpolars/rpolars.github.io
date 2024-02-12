

# Compute cosine

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/after-wrappers.R#L20)

## Description

Compute cosine

## Usage

<pre><code class='language-R'>Expr_cos()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(0, pi / 2, pi, NA_real_))$
  with_columns(cosine = pl$col("a")$cos())
```

    #> shape: (4, 2)
    #> ┌──────────┬────────────┐
    #> │ a        ┆ cosine     │
    #> │ ---      ┆ ---        │
    #> │ f64      ┆ f64        │
    #> ╞══════════╪════════════╡
    #> │ 0.0      ┆ 1.0        │
    #> │ 1.570796 ┆ 6.1232e-17 │
    #> │ 3.141593 ┆ -1.0       │
    #> │ null     ┆ null       │
    #> └──────────┴────────────┘
