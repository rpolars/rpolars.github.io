

# Get the number of unique values in a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/expr__list.R#L84)

## Description

Get the number of unique values in a list

## Usage

<pre><code class='language-R'>ExprList_n_unique()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(values = list(c(2, 2, NA), c(1, 2, 3), NA_real_))
df$with_columns(unique = pl$col("values")$list$n_unique())
```

    #> shape: (3, 2)
    #> ┌──────────────────┬────────┐
    #> │ values           ┆ unique │
    #> │ ---              ┆ ---    │
    #> │ list[f64]        ┆ u32    │
    #> ╞══════════════════╪════════╡
    #> │ [2.0, 2.0, null] ┆ 2      │
    #> │ [1.0, 2.0, 3.0]  ┆ 3      │
    #> │ [null]           ┆ 1      │
    #> └──────────────────┴────────┘
