

# Sort values in an array

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__array.R#L67)

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
Sort in descending order. When sorting by multiple columns, can be
specified per column by passing a vector of booleans.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprArr_sort_:_nulls_last">nulls_last</code>
</td>
<td>
If <code>TRUE</code>, place nulls values last.
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
