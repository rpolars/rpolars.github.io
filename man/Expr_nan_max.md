
# Get maximum value with NaN

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/#L)

## Description

Get maximum value, but returns <code>NaN</code> if there are any.

## Usage

<pre><code class='language-R'>Expr_nan_max
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(x = c(1, NA, 3, NaN, Inf))$
  with_columns(nan_max = pl$col("x")$nan_max())
```

    #> shape: (5, 2)
    #> ┌──────┬─────────┐
    #> │ x    ┆ nan_max │
    #> │ ---  ┆ ---     │
    #> │ f64  ┆ f64     │
    #> ╞══════╪═════════╡
    #> │ 1.0  ┆ NaN     │
    #> │ null ┆ NaN     │
    #> │ 3.0  ┆ NaN     │
    #> │ NaN  ┆ NaN     │
    #> │ inf  ┆ NaN     │
    #> └──────┴─────────┘
