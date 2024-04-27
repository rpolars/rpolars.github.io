

# Get the number of unique values in a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__list.R#L84)

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
