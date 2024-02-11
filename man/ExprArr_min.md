

# Find the minimum value in an array

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__array.R#L50)

## Description

Find the minimum value in an array

## Usage

<pre><code class='language-R'>ExprArr_min()
</code></pre>

## Details

This method is only available with the "simd" feature. See polars_info
for more details.

## Value

Expr

## Examples

``` r
library(polars)


df = pl$DataFrame(
  values = list(c(1, 2), c(3, 4), c(5, 6)),
  schema = list(values = pl$Array(pl$Float64, 2))
)
df$with_columns(min = pl$col("values")$arr$min())
```

    #> shape: (3, 2)
    #> ┌───────────────┬─────┐
    #> │ values        ┆ min │
    #> │ ---           ┆ --- │
    #> │ array[f64, 2] ┆ f64 │
    #> ╞═══════════════╪═════╡
    #> │ [1.0, 2.0]    ┆ 1.0 │
    #> │ [3.0, 4.0]    ┆ 3.0 │
    #> │ [5.0, 6.0]    ┆ 5.0 │
    #> └───────────────┴─────┘
