

# Sum all elements in a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/expr__list.R#L26)

## Description

Sum all elements in a list

## Usage

<pre><code class='language-R'>ExprList_sum()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(values = list(c(1, 2, 3, NA), c(2, 3), NA_real_)))
df$with_columns(sum = pl$col("values")$list$sum())
```

    #> shape: (3, 2)
    #> ┌────────────────────┬─────┐
    #> │ values             ┆ sum │
    #> │ ---                ┆ --- │
    #> │ list[f64]          ┆ f64 │
    #> ╞════════════════════╪═════╡
    #> │ [1.0, 2.0, … null] ┆ 6.0 │
    #> │ [2.0, 3.0]         ┆ 5.0 │
    #> │ [null]             ┆ 0.0 │
    #> └────────────────────┴─────┘
