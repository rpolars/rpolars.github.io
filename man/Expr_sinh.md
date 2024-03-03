

# Compute hyperbolic sine

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/after-wrappers.R#L20)

## Description

Compute hyperbolic sine

## Usage

<pre><code class='language-R'>Expr_sinh()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(-1, asinh(0.5), 0, 1, NA_real_))$
  with_columns(sinh = pl$col("a")$sinh())
```

    #> shape: (5, 2)
    #> ┌──────────┬───────────┐
    #> │ a        ┆ sinh      │
    #> │ ---      ┆ ---       │
    #> │ f64      ┆ f64       │
    #> ╞══════════╪═══════════╡
    #> │ -1.0     ┆ -1.175201 │
    #> │ 0.481212 ┆ 0.5       │
    #> │ 0.0      ┆ 0.0       │
    #> │ 1.0      ┆ 1.175201  │
    #> │ null     ┆ null      │
    #> └──────────┴───────────┘
