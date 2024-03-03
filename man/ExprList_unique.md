

# Get unique values in a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__list.R#L75)

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
