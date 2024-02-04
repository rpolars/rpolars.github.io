

# Find the minimum value in a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/expr__list.R#L44)

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
