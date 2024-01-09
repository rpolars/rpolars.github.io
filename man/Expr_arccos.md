
# Compute inverse cosine

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/#L)

## Description

Compute inverse cosine

## Usage

<pre><code class='language-R'>Expr_arccos
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
