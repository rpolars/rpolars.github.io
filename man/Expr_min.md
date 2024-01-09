
# Get minimum value

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/#L)

## Description

Get minimum value

## Usage

<pre><code class='language-R'>Expr_min
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(x = c(1, NA, 3))$
  with_columns(min = pl$col("x")$min())
```

    #> shape: (3, 2)
    #> ┌──────┬─────┐
    #> │ x    ┆ min │
    #> │ ---  ┆ --- │
    #> │ f64  ┆ f64 │
    #> ╞══════╪═════╡
    #> │ 1.0  ┆ 1.0 │
    #> │ null ┆ 1.0 │
    #> │ 3.0  ┆ 1.0 │
    #> └──────┴─────┘
