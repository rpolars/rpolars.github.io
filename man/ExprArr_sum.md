

# Sum all elements in an array

[**Source code**](https://github.com/pola-rs/r-polars/tree/mkdocs-matrial-search-preview/R/expr__array.R#L11)

## Description

Sum all elements in an array

## Usage

<pre><code class='language-R'>ExprArr_sum()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  values = list(c(1, 2), c(3, 4), c(NA_real_, 6)),
  schema = list(values = pl$Array(pl$Float64, 2))
)
df$with_columns(sum = pl$col("values")$arr$sum())
```

    #> shape: (3, 2)
    #> ┌───────────────┬─────┐
    #> │ values        ┆ sum │
    #> │ ---           ┆ --- │
    #> │ array[f64, 2] ┆ f64 │
    #> ╞═══════════════╪═════╡
    #> │ [1.0, 2.0]    ┆ 3.0 │
    #> │ [3.0, 4.0]    ┆ 7.0 │
    #> │ [null, 6.0]   ┆ 6.0 │
    #> └───────────────┴─────┘
