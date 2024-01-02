
# Floor

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/#L)

## Description

Rounds down to the nearest integer value. Only works on floating point
Series.

## Usage

<pre><code class='language-R'>Expr_floor
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(0.33, 0.5, 1.02, 1.5, NaN, NA, Inf, -Inf))$with_columns(
  floor = pl$col("a")$floor()
)
```

    #> shape: (8, 2)
    #> ┌──────┬───────┐
    #> │ a    ┆ floor │
    #> │ ---  ┆ ---   │
    #> │ f64  ┆ f64   │
    #> ╞══════╪═══════╡
    #> │ 0.33 ┆ 0.0   │
    #> │ 0.5  ┆ 0.0   │
    #> │ 1.02 ┆ 1.0   │
    #> │ 1.5  ┆ 1.0   │
    #> │ NaN  ┆ NaN   │
    #> │ null ┆ null  │
    #> │ inf  ┆ inf   │
    #> │ -inf ┆ -inf  │
    #> └──────┴───────┘
