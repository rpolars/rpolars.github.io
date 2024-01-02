
# Get maximum value

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/#L)

## Description

Get maximum value

## Usage

<pre><code class='language-R'>Expr_max
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(x = c(1, NA, 3))$
  with_columns(max = pl$col("x")$max())
```

    #> shape: (3, 2)
    #> ┌──────┬─────┐
    #> │ x    ┆ max │
    #> │ ---  ┆ --- │
    #> │ f64  ┆ f64 │
    #> ╞══════╪═════╡
    #> │ 1.0  ┆ 3.0 │
    #> │ null ┆ 3.0 │
    #> │ 3.0  ┆ 3.0 │
    #> └──────┴─────┘
