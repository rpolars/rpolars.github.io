

# Find the minimum value in a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/expr__list.R#L38)

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

df = pl$DataFrame(values = list(c(1, 2, 3, NA), c(2, 3), NA_real_))
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
