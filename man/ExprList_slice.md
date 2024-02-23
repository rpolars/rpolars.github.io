

# Slice list

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/expr__list.R#L310)

## Description

This extracts <code>length</code> values at most, starting at index
<code>offset</code>. This can return less than <code>length</code>
values if <code>length</code> is larger than the number of values.

## Usage

<pre><code class='language-R'>ExprList_slice(offset, length = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_slice_:_offset">offset</code>
</td>
<td>
Start index. Negative indexing is supported. Can be an Expr. Strings are
parsed as column names.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_slice_:_length">length</code>
</td>
<td>
Length of the slice. If <code>NULL</code> (default), the slice is taken
to the end of the list. Can be an Expr. Strings are parsed as column
names.
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
  idx_off = 1:2,
  len = c(4, 1)
)
df$with_columns(
  slice_by_expr = pl$col("s")$list$slice("idx_off", "len"),
  slice_by_lit = pl$col("s")$list$slice(2, 3)
)
```

    #> shape: (2, 5)
    #> ┌─────────────┬─────────┬─────┬───────────────┬──────────────┐
    #> │ s           ┆ idx_off ┆ len ┆ slice_by_expr ┆ slice_by_lit │
    #> │ ---         ┆ ---     ┆ --- ┆ ---           ┆ ---          │
    #> │ list[i32]   ┆ i32     ┆ f64 ┆ list[i32]     ┆ list[i32]    │
    #> ╞═════════════╪═════════╪═════╪═══════════════╪══════════════╡
    #> │ [1, 2, … 4] ┆ 1       ┆ 4.0 ┆ [2, 3, 4]     ┆ [3, 4]       │
    #> │ [10, 2, 1]  ┆ 2       ┆ 1.0 ┆ [1]           ┆ [1]          │
    #> └─────────────┴─────────┴─────┴───────────────┴──────────────┘
