

# Get unique values in a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/expr__list.R#L84)

## Description

Get the unique/distinct values in the list.

## Usage

<pre><code class='language-R'>ExprList_unique()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(values = list(c(2, 2, NA), c(1, 2, 3), NA_real_)))
df$with_columns(unique = pl$col("values")$list$unique())
```

    #> shape: (3, 2)
    #> ┌──────────────────┬─────────────────┐
    #> │ values           ┆ unique          │
    #> │ ---              ┆ ---             │
    #> │ list[f64]        ┆ list[f64]       │
    #> ╞══════════════════╪═════════════════╡
    #> │ [2.0, 2.0, null] ┆ [null, 2.0]     │
    #> │ [1.0, 2.0, 3.0]  ┆ [1.0, 2.0, 3.0] │
    #> │ [null]           ┆ [null]          │
    #> └──────────────────┴─────────────────┘
