

# Join elements of a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/expr__list.R#L251)

## Description

Join all string items in a sublist and place a separator between them.
This only works on columns of type <code>list\[str\]</code>.

## Usage

<pre><code class='language-R'>ExprList_join(separator, ignore_nulls = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_join_:_separator">separator</code>
</td>
<td>
String to separate the items with. Can be an Expr. Strings are
<em>not</em> parsed as columns.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_join_:_ignore_nulls">ignore_nulls</code>
</td>
<td>
If <code>FALSE</code> (default), null values are propagated: if the row
contains any null values, the output is null.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  s = list(c("a", "b", "c"), c("x", "y"), c("e", NA)),
  separator = c("-", "+", "/")
)
df$with_columns(
  join_with_expr = pl$col("s")$list$join(pl$col("separator")),
  join_with_lit = pl$col("s")$list$join(" "),
  join_ignore_null = pl$col("s")$list$join(" ", ignore_nulls = TRUE)
)
```

    #> shape: (3, 5)
    #> ┌─────────────────┬───────────┬────────────────┬───────────────┬──────────────────┐
    #> │ s               ┆ separator ┆ join_with_expr ┆ join_with_lit ┆ join_ignore_null │
    #> │ ---             ┆ ---       ┆ ---            ┆ ---           ┆ ---              │
    #> │ list[str]       ┆ str       ┆ str            ┆ str           ┆ str              │
    #> ╞═════════════════╪═══════════╪════════════════╪═══════════════╪══════════════════╡
    #> │ ["a", "b", "c"] ┆ -         ┆ a-b-c          ┆ a b c         ┆ a b c            │
    #> │ ["x", "y"]      ┆ +         ┆ x+y            ┆ x y           ┆ x y              │
    #> │ ["e", null]     ┆ /         ┆ null           ┆ null          ┆ e                │
    #> └─────────────────┴───────────┴────────────────┴───────────────┴──────────────────┘
