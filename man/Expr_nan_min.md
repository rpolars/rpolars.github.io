

# Get minimum value with NaN

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/after-wrappers.R#L20)

## Description

Get minimum value, but returns <code>NaN</code> if there are any.

## Usage

<pre><code class='language-R'>Expr_nan_min()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(x = c(1, NA, 3, NaN, Inf))$
  with_columns(nan_min = pl$col("x")$nan_min())
```

    #> shape: (5, 2)
    #> ┌──────┬─────────┐
    #> │ x    ┆ nan_min │
    #> │ ---  ┆ ---     │
    #> │ f64  ┆ f64     │
    #> ╞══════╪═════════╡
    #> │ 1.0  ┆ NaN     │
    #> │ null ┆ NaN     │
    #> │ 3.0  ┆ NaN     │
    #> │ NaN  ┆ NaN     │
    #> │ inf  ┆ NaN     │
    #> └──────┴─────────┘
