

# Reverse values in a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__list.R#L66)

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

df = pl$DataFrame(values = list(c(1, 2, 3, NA), c(2, 3), NA_real_))
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
