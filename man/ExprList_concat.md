
# Concat two list variables

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__list.R#L103)

## Description

Concat two list variables

## Usage

<pre><code class='language-R'>ExprList_concat(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_concat_:_other">other</code>
</td>
<td>
Values to concat with. Can be an Expr or something coercible to an Expr.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = list("a", "x"),
  b = list(c("b", "c"), c("y", "z"))
)
df$with_columns(
  conc_to_b = pl$col("a")$list$concat(pl$col("b")),
  conc_to_lit_str = pl$col("a")$list$concat(pl$lit("some string")),
  conc_to_lit_list = pl$col("a")$list$concat(pl$lit(list("hello", c("hello", "world"))))
)
```

    #> shape: (2, 5)
    #> ┌───────────┬────────────┬─────────────────┬──────────────────────┬─────────────────────────┐
    #> │ a         ┆ b          ┆ conc_to_b       ┆ conc_to_lit_str      ┆ conc_to_lit_list        │
    #> │ ---       ┆ ---        ┆ ---             ┆ ---                  ┆ ---                     │
    #> │ list[str] ┆ list[str]  ┆ list[str]       ┆ list[str]            ┆ list[str]               │
    #> ╞═══════════╪════════════╪═════════════════╪══════════════════════╪═════════════════════════╡
    #> │ ["a"]     ┆ ["b", "c"] ┆ ["a", "b", "c"] ┆ ["a", "some string"] ┆ ["a", "hello"]          │
    #> │ ["x"]     ┆ ["y", "z"] ┆ ["x", "y", "z"] ┆ ["x", "some string"] ┆ ["x", "hello", "world"] │
    #> └───────────┴────────────┴─────────────────┴──────────────────────┴─────────────────────────┘
