

# Compute inverse cosine

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/after-wrappers.R#L20)

## Description

Compute inverse cosine

## Usage

<pre><code class='language-R'>Expr_arccos()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(-1, cos(0.5), 0, 1, NA_real_))$
  with_columns(arccos = pl$col("a")$arccos())
```

    #> shape: (5, 2)
    #> ┌──────────┬──────────┐
    #> │ a        ┆ arccos   │
    #> │ ---      ┆ ---      │
    #> │ f64      ┆ f64      │
    #> ╞══════════╪══════════╡
    #> │ -1.0     ┆ 3.141593 │
    #> │ 0.877583 ┆ 0.5      │
    #> │ 0.0      ┆ 1.570796 │
    #> │ 1.0      ┆ 0.0      │
    #> │ null     ┆ null     │
    #> └──────────┴──────────┘
