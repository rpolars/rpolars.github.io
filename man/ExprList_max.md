
# Find the maximum value in a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__list.R#L35)

## Description

Find the maximum value in a list

## Usage

<pre><code class='language-R'>ExprList_max()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(values = list(c(1, 2, 3, NA), c(2, 3), NA_real_)))
df$with_columns(max = pl$col("values")$list$max())
```

    #> shape: (3, 2)
    #> ┌────────────────────┬──────┐
    #> │ values             ┆ max  │
    #> │ ---                ┆ ---  │
    #> │ list[f64]          ┆ f64  │
    #> ╞════════════════════╪══════╡
    #> │ [1.0, 2.0, … null] ┆ 3.0  │
    #> │ [2.0, 3.0]         ┆ 3.0  │
    #> │ [null]             ┆ null │
    #> └────────────────────┴──────┘
