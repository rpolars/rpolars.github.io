

# Ceiling

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/after-wrappers.R#L20)

## Description

Rounds up to the nearest integer value. Only works on floating point
Series.

## Usage

<pre><code class='language-R'>Expr_ceil()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(0.33, 0.5, 1.02, 1.5, NaN, NA, Inf, -Inf))$with_columns(
  ceiling = pl$col("a")$ceil()
)
```

    #> shape: (8, 2)
    #> ┌──────┬─────────┐
    #> │ a    ┆ ceiling │
    #> │ ---  ┆ ---     │
    #> │ f64  ┆ f64     │
    #> ╞══════╪═════════╡
    #> │ 0.33 ┆ 1.0     │
    #> │ 0.5  ┆ 1.0     │
    #> │ 1.02 ┆ 2.0     │
    #> │ 1.5  ┆ 2.0     │
    #> │ NaN  ┆ NaN     │
    #> │ null ┆ null    │
    #> │ inf  ┆ inf     │
    #> │ -inf ┆ -inf    │
    #> └──────┴─────────┘
