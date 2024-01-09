
# Get maximum value

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/#L)

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
