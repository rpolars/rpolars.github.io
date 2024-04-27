

# Sort an Expr

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__expr.R#L1385)

## Description

Sort this column. If used in a groupby context, the groups are sorted.

## Usage

<pre><code class='language-R'>Expr_sort(..., descending = FALSE, nulls_last = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
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

## Examples

``` r
library(polars)

pl$DataFrame(a = c(6, 1, 0, NA, Inf, NaN))$
  with_columns(sorted = pl$col("a")$sort())
```

    #> shape: (6, 2)
    #> ┌──────┬────────┐
    #> │ a    ┆ sorted │
    #> │ ---  ┆ ---    │
    #> │ f64  ┆ f64    │
    #> ╞══════╪════════╡
    #> │ 6.0  ┆ null   │
    #> │ 1.0  ┆ 0.0    │
    #> │ 0.0  ┆ 1.0    │
    #> │ null ┆ 6.0    │
    #> │ inf  ┆ inf    │
    #> │ NaN  ┆ NaN    │
    #> └──────┴────────┘
