

# Get the last <code>n</code> values of a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__list.R#L397)

## Description

Get the last <code>n</code> values of a list

## Usage

<pre><code class='language-R'>ExprList_tail(n = 5L)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_tail_:_n">n</code>
</td>
<td>
Number of values to return for each sublist. Can be an Expr. Strings are
parsed as column names.
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
  n = 1:2
)
df$with_columns(
  tail_by_expr = pl$col("s")$list$tail("n"),
  tail_by_lit = pl$col("s")$list$tail(2)
)
```

    #> shape: (2, 4)
    #> ┌─────────────┬─────┬──────────────┬─────────────┐
    #> │ s           ┆ n   ┆ tail_by_expr ┆ tail_by_lit │
    #> │ ---         ┆ --- ┆ ---          ┆ ---         │
    #> │ list[i32]   ┆ i32 ┆ list[i32]    ┆ list[i32]   │
    #> ╞═════════════╪═════╪══════════════╪═════════════╡
    #> │ [1, 2, … 4] ┆ 1   ┆ [4]          ┆ [3, 4]      │
    #> │ [10, 2, 1]  ┆ 2   ┆ [2, 1]       ┆ [2, 1]      │
    #> └─────────────┴─────┴──────────────┴─────────────┘
