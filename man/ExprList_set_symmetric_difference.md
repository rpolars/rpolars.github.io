

# Get the symmetric difference of two list variables

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/expr__list.R#L598)

## Description

This returns all elements that are in only one of the two lists. To get
only elements that are in the first list but not in the second one, use
<code>$set_difference()</code>.

## Usage

<pre><code class='language-R'>ExprList_set_symmetric_difference(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_set_symmetric_difference_:_other">other</code>
</td>
<td>
Other list variable. Can be an Expr or something coercible to an Expr.
</td>
</tr>
</table>

## Details

Note that the datatypes inside the list must have a common supertype.
For example, the first column can be <code>list\[i32\]</code> and the
second one can be <code>list\[i8\]</code> because it can be cast to
<code>list\[i32\]</code>. However, the second column cannot be e.g
<code>list\[f32\]</code>.

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = list(1:3, NA_integer_, c(NA_integer_, 3L), 5:7),
  b = list(2:4, 3L, c(3L, 4L, NA_integer_), c(6L, 8L))
)

df$with_columns(
  symmetric_difference = pl$col("a")$list$set_symmetric_difference("b")
)
```

    #> shape: (4, 3)
    #> ┌───────────┬──────────────┬──────────────────────┐
    #> │ a         ┆ b            ┆ symmetric_difference │
    #> │ ---       ┆ ---          ┆ ---                  │
    #> │ list[i32] ┆ list[i32]    ┆ list[i32]            │
    #> ╞═══════════╪══════════════╪══════════════════════╡
    #> │ [1, 2, 3] ┆ [2, 3, 4]    ┆ [1, 4]               │
    #> │ [null]    ┆ [3]          ┆ [null, 3]            │
    #> │ [null, 3] ┆ [3, 4, null] ┆ [4]                  │
    #> │ [5, 6, 7] ┆ [6, 8]       ┆ [5, 7, 8]            │
    #> └───────────┴──────────────┴──────────────────────┘
