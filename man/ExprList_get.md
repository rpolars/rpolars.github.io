

# Get the value by index in a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/expr__list.R#L131)

## Description

This allows to extract one value per list only. To extract several
values by index, use <code>$list$gather()</code>.

## Usage

<pre><code class='language-R'>ExprList_get(index)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_get_:_index">index</code>
</td>
<td>
An Expr or something coercible to an Expr, that must return a single
index. Values are 0-indexed (so index 0 would return the first item of
every sublist) and negative values start from the end (index
<code>-1</code> returns the last item). If the index is out of bounds,
it will return a <code>null</code>. Strings are parsed as column names.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  values = list(c(2, 2, NA), c(1, 2, 3), NA_real_, NULL),
  idx = c(1, 2, NA, 3)
)
df$with_columns(
  using_expr = pl$col("values")$list$get("idx"),
  val_0 = pl$col("values")$list$get(0),
  val_minus_1 = pl$col("values")$list$get(-1),
  val_oob = pl$col("values")$list$get(10)
)
```

    #> shape: (4, 6)
    #> ┌──────────────────┬──────┬────────────┬───────┬─────────────┬─────────┐
    #> │ values           ┆ idx  ┆ using_expr ┆ val_0 ┆ val_minus_1 ┆ val_oob │
    #> │ ---              ┆ ---  ┆ ---        ┆ ---   ┆ ---         ┆ ---     │
    #> │ list[f64]        ┆ f64  ┆ f64        ┆ f64   ┆ f64         ┆ f64     │
    #> ╞══════════════════╪══════╪════════════╪═══════╪═════════════╪═════════╡
    #> │ [2.0, 2.0, null] ┆ 1.0  ┆ 2.0        ┆ 2.0   ┆ null        ┆ null    │
    #> │ [1.0, 2.0, 3.0]  ┆ 2.0  ┆ 3.0        ┆ 1.0   ┆ 3.0         ┆ null    │
    #> │ [null]           ┆ null ┆ null       ┆ null  ┆ null        ┆ null    │
    #> │ []               ┆ 3.0  ┆ null       ┆ null  ┆ null        ┆ null    │
    #> └──────────────────┴──────┴────────────┴───────┴─────────────┴─────────┘
