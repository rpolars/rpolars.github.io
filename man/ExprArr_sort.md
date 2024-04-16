

# Sort values in an array

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/expr__array.R#L103)

## Description

Sort values in an array

## Usage

<pre><code class='language-R'>ExprArr_sort(descending = FALSE, nulls_last = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprArr_sort_:_descending">descending</code>
</td>
<td>
A logical. If <code>TRUE</code>, sort in descending order.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprArr_sort_:_nulls_last">nulls_last</code>
</td>
<td>
A logical. If <code>TRUE</code>, place <code>null</code> values last
insead of first.
</td>
</tr>
</table>

## Examples

``` r
library(polars)

df = pl$DataFrame(
  values = list(c(2, 1), c(3, 4), c(NA_real_, 6)),
  schema = list(values = pl$Array(pl$Float64, 2))
)
df$with_columns(sort = pl$col("values")$arr$sort(nulls_last = TRUE))
```

    #> shape: (3, 2)
    #> ┌───────────────┬───────────────┐
    #> │ values        ┆ sort          │
    #> │ ---           ┆ ---           │
    #> │ array[f64, 2] ┆ array[f64, 2] │
    #> ╞═══════════════╪═══════════════╡
    #> │ [2.0, 1.0]    ┆ [1.0, 2.0]    │
    #> │ [3.0, 4.0]    ┆ [3.0, 4.0]    │
    #> │ [null, 6.0]   ┆ [6.0, null]   │
    #> └───────────────┴───────────────┘
