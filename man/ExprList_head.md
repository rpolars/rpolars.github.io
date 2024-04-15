

# Get the first <code>n</code> values of a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/expr__list.R#L377)

## Description

Get the first <code>n</code> values of a list

## Usage

<pre><code class='language-R'>ExprList_head(n = 5L)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_head_:_n">n</code>
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
  head_by_expr = pl$col("s")$list$head("n"),
  head_by_lit = pl$col("s")$list$head(2)
)
```

    #> shape: (2, 4)
    #> ┌─────────────┬─────┬──────────────┬─────────────┐
    #> │ s           ┆ n   ┆ head_by_expr ┆ head_by_lit │
    #> │ ---         ┆ --- ┆ ---          ┆ ---         │
    #> │ list[i32]   ┆ i32 ┆ list[i32]    ┆ list[i32]   │
    #> ╞═════════════╪═════╪══════════════╪═════════════╡
    #> │ [1, 2, … 4] ┆ 1   ┆ [1]          ┆ [1, 2]      │
    #> │ [10, 2, 1]  ┆ 2   ┆ [10, 2]      ┆ [10, 2]     │
    #> └─────────────┴─────┴──────────────┴─────────────┘
