

# Find the minimum value in a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/expr__list.R#L44)

## Description

Find the minimum value in a list

## Usage

<pre><code class='language-R'>ExprList_min()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(values = list(c(1, 2, 3, NA), c(2, 3), NA_real_)))
df$with_columns(min = pl$col("values")$list$min())
```

    #> shape: (3, 2)
    #> ┌────────────────────┬──────┐
    #> │ values             ┆ min  │
    #> │ ---                ┆ ---  │
    #> │ list[f64]          ┆ f64  │
    #> ╞════════════════════╪══════╡
    #> │ [1.0, 2.0, … null] ┆ 1.0  │
    #> │ [2.0, 3.0]         ┆ 2.0  │
    #> │ [null]             ┆ null │
    #> └────────────────────┴──────┘
