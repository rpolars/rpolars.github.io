

# Index of max value

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/after-wrappers.R#L20)

## Description

Get the index of the maximal value.

## Usage

<pre><code class='language-R'>Expr_arg_max()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(
  a = c(6, 1, 0, NA, Inf, NaN)
)$with_columns(arg_max = pl$col("a")$arg_max())
```

    #> shape: (6, 2)
    #> ┌──────┬─────────┐
    #> │ a    ┆ arg_max │
    #> │ ---  ┆ ---     │
    #> │ f64  ┆ u32     │
    #> ╞══════╪═════════╡
    #> │ 6.0  ┆ 4       │
    #> │ 1.0  ┆ 4       │
    #> │ 0.0  ┆ 4       │
    #> │ null ┆ 4       │
    #> │ inf  ┆ 4       │
    #> │ NaN  ┆ 4       │
    #> └──────┴─────────┘
