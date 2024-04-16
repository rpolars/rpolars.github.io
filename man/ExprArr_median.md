

# Find the median in an array

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/expr__array.R#L59)

## Description

Find the median in an array

## Usage

<pre><code class='language-R'>ExprArr_median()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  values = list(c(2, 1, 4), c(8.4, 3.2, 1)),
  schema = list(values = pl$Array(pl$Float64, 3))
)
df$with_columns(median = pl$col("values")$arr$median())
```

    #> shape: (2, 2)
    #> ┌─────────────────┬────────┐
    #> │ values          ┆ median │
    #> │ ---             ┆ ---    │
    #> │ array[f64, 3]   ┆ f64    │
    #> ╞═════════════════╪════════╡
    #> │ [2.0, 1.0, 4.0] ┆ 2.0    │
    #> │ [8.4, 3.2, 1.0] ┆ 3.2    │
    #> └─────────────────┴────────┘
