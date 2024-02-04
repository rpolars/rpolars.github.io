

# Reverse values in a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/expr__list.R#L72)

## Description

Reverse values in a list

## Usage

<pre><code class='language-R'>ExprList_reverse()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(values = list(c(1, 2, 3, NA), c(2, 3), NA_real_)))
df$with_columns(reverse = pl$col("values")$list$reverse())
```

    #> shape: (3, 2)
    #> ┌────────────────────┬────────────────────┐
    #> │ values             ┆ reverse            │
    #> │ ---                ┆ ---                │
    #> │ list[f64]          ┆ list[f64]          │
    #> ╞════════════════════╪════════════════════╡
    #> │ [1.0, 2.0, … null] ┆ [null, 3.0, … 1.0] │
    #> │ [2.0, 3.0]         ┆ [3.0, 2.0]         │
    #> │ [null]             ┆ [null]             │
    #> └────────────────────┴────────────────────┘
