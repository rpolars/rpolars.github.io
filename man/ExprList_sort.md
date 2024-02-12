

# Sort values in a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/expr__list.R#L57)

## Description

Sort values in a list

## Usage

<pre><code class='language-R'>ExprList_sort(descending = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_sort_:_descending">descending</code>
</td>
<td>
Sort values in descending order
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(values = list(c(1, 2, 3, NA), c(2, 3), NA_real_)))
df$with_columns(sort = pl$col("values")$list$sort())
```

    #> shape: (3, 2)
    #> ┌────────────────────┬────────────────────┐
    #> │ values             ┆ sort               │
    #> │ ---                ┆ ---                │
    #> │ list[f64]          ┆ list[f64]          │
    #> ╞════════════════════╪════════════════════╡
    #> │ [1.0, 2.0, … null] ┆ [null, 1.0, … 3.0] │
    #> │ [2.0, 3.0]         ┆ [2.0, 3.0]         │
    #> │ [null]             ┆ [null]             │
    #> └────────────────────┴────────────────────┘
