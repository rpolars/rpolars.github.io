
# Compute the base-10 logarithm of elements

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/#L)

## Description

Compute the base-10 logarithm of elements

## Usage

<pre><code class='language-R'>Expr_log10
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(1, 2, 3, exp(1)))$
  with_columns(log10 = pl$col("a")$log10())
```

    #> shape: (4, 2)
    #> ┌──────────┬──────────┐
    #> │ a        ┆ log10    │
    #> │ ---      ┆ ---      │
    #> │ f64      ┆ f64      │
    #> ╞══════════╪══════════╡
    #> │ 1.0      ┆ 0.0      │
    #> │ 2.0      ┆ 0.30103  │
    #> │ 3.0      ┆ 0.477121 │
    #> │ 2.718282 ┆ 0.434294 │
    #> └──────────┴──────────┘
