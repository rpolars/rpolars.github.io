
# Join elements of a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__list.R#L222)

## Description

Join all string items in a sublist and place a separator between them.
This only works on columns of type <code>list\[str\]</code>.

## Usage

<pre><code class='language-R'>ExprList_join(separator)
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
  join_with_lit = pl$col("s")$list$join(" ")
)
```

    #> shape: (3, 4)
    #> ┌─────────────────┬───────────┬────────────────┬───────────────┐
    #> │ s               ┆ separator ┆ join_with_expr ┆ join_with_lit │
    #> │ ---             ┆ ---       ┆ ---            ┆ ---           │
    #> │ list[str]       ┆ str       ┆ str            ┆ str           │
    #> ╞═════════════════╪═══════════╪════════════════╪═══════════════╡
    #> │ ["a", "b", "c"] ┆ -         ┆ a-b-c          ┆ a b c         │
    #> │ ["x", "y"]      ┆ +         ┆ x+y            ┆ x y           │
    #> │ ["e", null]     ┆ /         ┆ e/null         ┆ e null        │
    #> └─────────────────┴───────────┴────────────────┴───────────────┘
