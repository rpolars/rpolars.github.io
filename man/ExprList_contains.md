

# Check if list contains a given value

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__list.R#L228)

## Description

Check if list contains a given value

## Usage

<pre><code class='language-R'>ExprList_contains(item)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_contains_:_item">item</code>
</td>
<td>
Expr or something coercible to an Expr. Strings are <em>not</em> parsed
as columns.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = list(3:1, NULL, 1:2),
  item = 0:2
)
df$with_columns(
  with_expr = pl$col("a")$list$contains(pl$col("item")),
  with_lit = pl$col("a")$list$contains(1)
)
```

    #> shape: (3, 4)
    #> ┌───────────┬──────┬───────────┬──────────┐
    #> │ a         ┆ item ┆ with_expr ┆ with_lit │
    #> │ ---       ┆ ---  ┆ ---       ┆ ---      │
    #> │ list[i32] ┆ i32  ┆ bool      ┆ bool     │
    #> ╞═══════════╪══════╪═══════════╪══════════╡
    #> │ [3, 2, 1] ┆ 0    ┆ false     ┆ true     │
    #> │ []        ┆ 1    ┆ false     ┆ false    │
    #> │ [1, 2]    ┆ 2    ┆ true      ┆ true     │
    #> └───────────┴──────┴───────────┴──────────┘
