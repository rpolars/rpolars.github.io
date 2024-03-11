

# Get unique values in a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/expr__list.R#L75)

## Description

Get unique values in a list

## Usage

<pre><code class='language-R'>ExprList_unique()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(values = list(c(2, 2, NA), c(1, 2, 3), NA_real_))
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
