

# Shift array values by <code>n</code> indices

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__array.R#L276)

## Description

Shift array values by <code>n</code> indices

## Usage

<pre><code class='language-R'>ExprArr_shift(periods = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprArr_shift_:_periods">periods</code>
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
  values = list(1:3, c(2L, NA_integer_, 5L)),
  idx = 1:2,
  schema = list(values = pl$Array(pl$Int32, 3))
)
df$with_columns(
  shift_by_expr = pl$col("values")$arr$shift(pl$col("idx")),
  shift_by_lit = pl$col("values")$arr$shift(2)
)
```

    #> shape: (2, 4)
    #> ┌───────────────┬─────┬─────────────────┬─────────────────┐
    #> │ values        ┆ idx ┆ shift_by_expr   ┆ shift_by_lit    │
    #> │ ---           ┆ --- ┆ ---             ┆ ---             │
    #> │ array[i32, 3] ┆ i32 ┆ array[i32, 3]   ┆ array[i32, 3]   │
    #> ╞═══════════════╪═════╪═════════════════╪═════════════════╡
    #> │ [1, 2, 3]     ┆ 1   ┆ [null, 1, 2]    ┆ [null, null, 1] │
    #> │ [2, null, 5]  ┆ 2   ┆ [null, null, 2] ┆ [null, null, 2] │
    #> └───────────────┴─────┴─────────────────┴─────────────────┘
