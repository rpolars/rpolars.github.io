

# Get the difference of two list variables

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/expr__list.R#L530)

## Description

This returns the "asymmetric difference", meaning only the elements of
the first list that are not in the second list. To get all elements that
are in only one of the two lists, use
<code>$set_symmetric_difference()</code>.

## Usage

<pre><code class='language-R'>ExprList_set_difference(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_set_difference_:_other">other</code>
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

df$with_columns(difference = pl$col("a")$list$set_difference("b"))
```

    #> shape: (4, 3)
    #> ┌───────────┬──────────────┬────────────┐
    #> │ a         ┆ b            ┆ difference │
    #> │ ---       ┆ ---          ┆ ---        │
    #> │ list[i32] ┆ list[i32]    ┆ list[i32]  │
    #> ╞═══════════╪══════════════╪════════════╡
    #> │ [1, 2, 3] ┆ [2, 3, 4]    ┆ [1]        │
    #> │ [null]    ┆ [3]          ┆ [null]     │
    #> │ [null, 3] ┆ [3, 4, null] ┆ []         │
    #> │ [5, 6, 7] ┆ [6, 8]       ┆ [5, 7]     │
    #> └───────────┴──────────────┴────────────┘
