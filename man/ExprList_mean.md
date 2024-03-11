

# Compute the mean value of a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/expr__list.R#L47)

## Description

Compute the mean value of a list

## Usage

<pre><code class='language-R'>ExprList_mean()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(values = list(c(1, 2, 3, NA), c(2, 3), NA_real_))
df$with_columns(mean = pl$col("values")$list$mean())
```

    #> shape: (3, 2)
    #> ┌────────────────────┬──────┐
    #> │ values             ┆ mean │
    #> │ ---                ┆ ---  │
    #> │ list[f64]          ┆ f64  │
    #> ╞════════════════════╪══════╡
    #> │ [1.0, 2.0, … null] ┆ 2.0  │
    #> │ [2.0, 3.0]         ┆ 2.5  │
    #> │ [null]             ┆ null │
    #> └────────────────────┴──────┘
