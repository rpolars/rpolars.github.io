
# Get minimum value with NaN

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/#L)

## Description

Get minimum value, but returns <code>NaN</code> if there are any.

## Usage

<pre><code class='language-R'>Expr_nan_min
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
