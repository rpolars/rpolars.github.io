

# Index of min value

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/after-wrappers.R#L20)

## Description

Get the index of the minimal value.

## Usage

<pre><code class='language-R'>Expr_arg_min()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(
  a = c(6, 1, 0, NA, Inf, NaN)
)$with_columns(arg_min = pl$col("a")$arg_min())
```

    #> shape: (6, 2)
    #> ┌──────┬─────────┐
    #> │ a    ┆ arg_min │
    #> │ ---  ┆ ---     │
    #> │ f64  ┆ u32     │
    #> ╞══════╪═════════╡
    #> │ 6.0  ┆ 2       │
    #> │ 1.0  ┆ 2       │
    #> │ 0.0  ┆ 2       │
    #> │ null ┆ 2       │
    #> │ inf  ┆ 2       │
    #> │ NaN  ┆ 2       │
    #> └──────┴─────────┘
