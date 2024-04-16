

# Shift list values by <code>n</code> indices

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/expr__list.R#L328)

## Description

Shift list values by <code>n</code> indices

## Usage

<pre><code class='language-R'>ExprList_shift(periods = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_shift_:_periods">periods</code>
</td>
<td>
Number of places to shift (may be negative). Can be an Expr. Strings are
<em>not</em> parsed as columns.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  s = list(1:4, c(10L, 2L, 1L)),
  idx = 1:2
)
df$with_columns(
  shift_by_expr = pl$col("s")$list$shift(pl$col("idx")),
  shift_by_lit = pl$col("s")$list$shift(2)
)
```

    #> shape: (2, 4)
    #> ┌─────────────┬─────┬──────────────────┬───────────────────┐
    #> │ s           ┆ idx ┆ shift_by_expr    ┆ shift_by_lit      │
    #> │ ---         ┆ --- ┆ ---              ┆ ---               │
    #> │ list[i32]   ┆ i32 ┆ list[i32]        ┆ list[i32]         │
    #> ╞═════════════╪═════╪══════════════════╪═══════════════════╡
    #> │ [1, 2, … 4] ┆ 1   ┆ [null, 1, … 3]   ┆ [null, null, … 2] │
    #> │ [10, 2, 1]  ┆ 2   ┆ [null, null, 10] ┆ [null, null, 10]  │
    #> └─────────────┴─────┴──────────────────┴───────────────────┘
