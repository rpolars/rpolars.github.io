

# Join elements of an array

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/expr__array.R#L205)

## Description

Join all string items in a sub-array and place a separator between them.
This only works on columns of type <code>list\[str\]</code>.

## Usage

<pre><code class='language-R'>ExprArr_join(separator, ignore_nulls = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprArr_join_:_separator">separator</code>
</td>
<td>
String to separate the items with. Can be an Expr. Strings are
<em>not</em> parsed as columns.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprArr_join_:_ignore_nulls">ignore_nulls</code>
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
  values = list(c("a", "b", "c"), c("x", "y", "z"), c("e", NA, NA)),
  separator = c("-", "+", "/"),
  schema = list(values = pl$Array(pl$String, 3))
)
df$with_columns(
  join_with_expr = pl$col("values")$arr$join(pl$col("separator")),
  join_with_lit = pl$col("values")$arr$join(" "),
  join_ignore_null = pl$col("values")$arr$join(" ", ignore_nulls = TRUE)
)
```

    #> shape: (3, 5)
    #> ┌───────────────────┬───────────┬────────────────┬───────────────┬──────────────────┐
    #> │ values            ┆ separator ┆ join_with_expr ┆ join_with_lit ┆ join_ignore_null │
    #> │ ---               ┆ ---       ┆ ---            ┆ ---           ┆ ---              │
    #> │ array[str, 3]     ┆ str       ┆ str            ┆ str           ┆ str              │
    #> ╞═══════════════════╪═══════════╪════════════════╪═══════════════╪══════════════════╡
    #> │ ["a", "b", "c"]   ┆ -         ┆ a-b-c          ┆ a b c         ┆ a b c            │
    #> │ ["x", "y", "z"]   ┆ +         ┆ x+y+z          ┆ x y z         ┆ x y z            │
    #> │ ["e", null, null] ┆ /         ┆ null           ┆ null          ┆ e                │
    #> └───────────────────┴───────────┴────────────────┴───────────────┴──────────────────┘
