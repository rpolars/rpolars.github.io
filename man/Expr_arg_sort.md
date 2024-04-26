

# Index of a sort

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L1429)

## Description

Get the index values that would sort this column.

## Usage

<pre><code class='language-R'>Expr_arg_sort(descending = FALSE, nulls_last = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="descending">descending</code>
</td>
<td>
A logical. If <code>TRUE</code>, sort in descending order.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="nulls_last">nulls_last</code>
</td>
<td>
A logical. If <code>TRUE</code>, place <code>null</code> values last
insead of first.
</td>
</tr>
</table>

## Value

Expr

## See Also

pl$arg_sort_by() to find the row indices that would sort multiple
columns.

## Examples

``` r
library(polars)

pl$DataFrame(
  a = c(6, 1, 0, NA, Inf, NaN)
)$with_columns(arg_sorted = pl$col("a")$arg_sort())
```

    #> shape: (6, 2)
    #> ┌──────┬────────────┐
    #> │ a    ┆ arg_sorted │
    #> │ ---  ┆ ---        │
    #> │ f64  ┆ u32        │
    #> ╞══════╪════════════╡
    #> │ 6.0  ┆ 3          │
    #> │ 1.0  ┆ 2          │
    #> │ 0.0  ┆ 1          │
    #> │ null ┆ 0          │
    #> │ inf  ┆ 4          │
    #> │ NaN  ┆ 5          │
    #> └──────┴────────────┘
