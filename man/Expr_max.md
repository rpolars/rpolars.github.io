

# Get maximum value

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/after-wrappers.R#L20)

## Description

Get maximum value

## Usage

<pre><code class='language-R'>Expr_max()
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
