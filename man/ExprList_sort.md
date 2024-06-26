

# Sort values in a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__list.R#L57)

## Description

Sort values in a list

## Usage

<pre><code class='language-R'>ExprList_sort(descending = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="descending">descending</code>
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

df = pl$DataFrame(values = list(c(NA, 2, 1, 3), c(Inf, 2, 3, NaN), NA_real_))
df$with_columns(sort = pl$col("values")$list$sort())
```

    #> shape: (3, 2)
    #> ┌────────────────────┬────────────────────┐
    #> │ values             ┆ sort               │
    #> │ ---                ┆ ---                │
    #> │ list[f64]          ┆ list[f64]          │
    #> ╞════════════════════╪════════════════════╡
    #> │ [null, 2.0, … 3.0] ┆ [null, 1.0, … 3.0] │
    #> │ [inf, 2.0, … NaN]  ┆ [2.0, 3.0, … NaN]  │
    #> │ [null]             ┆ [null]             │
    #> └────────────────────┴────────────────────┘
