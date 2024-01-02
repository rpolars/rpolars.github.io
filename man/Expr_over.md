
# Apply window function over a subgroup

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/expr__expr.R#L1920)

## Description

This applies an expression on groups and returns the same number of rows
as the input (contrarily to
<code style="white-space: pre;">$group_by()</code> +
<code style="white-space: pre;">$agg()</code>).

## Usage

<pre><code class='language-R'>Expr_over(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_over_:_...">…</code>
</td>
<td>
Character vector indicating the columns to group by.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(
  val = 1:5,
  a = c("+", "+", "-", "-", "+"),
  b = c("+", "-", "+", "-", "+")
)$with_columns(
  count = pl$col("val")$count()$over("a", "b")
)
```

    #> shape: (5, 4)
    #> ┌─────┬─────┬─────┬───────┐
    #> │ val ┆ a   ┆ b   ┆ count │
    #> │ --- ┆ --- ┆ --- ┆ ---   │
    #> │ i32 ┆ str ┆ str ┆ u32   │
    #> ╞═════╪═════╪═════╪═══════╡
    #> │ 1   ┆ +   ┆ +   ┆ 2     │
    #> │ 2   ┆ +   ┆ -   ┆ 1     │
    #> │ 3   ┆ -   ┆ +   ┆ 1     │
    #> │ 4   ┆ -   ┆ -   ┆ 1     │
    #> │ 5   ┆ +   ┆ +   ┆ 2     │
    #> └─────┴─────┴─────┴───────┘

``` r
over_vars = c("a", "b")
pl$DataFrame(
  val = 1:5,
  a = c("+", "+", "-", "-", "+"),
  b = c("+", "-", "+", "-", "+")
)$with_columns(
  count = pl$col("val")$count()$over(over_vars)
)
```

    #> shape: (5, 4)
    #> ┌─────┬─────┬─────┬───────┐
    #> │ val ┆ a   ┆ b   ┆ count │
    #> │ --- ┆ --- ┆ --- ┆ ---   │
    #> │ i32 ┆ str ┆ str ┆ u32   │
    #> ╞═════╪═════╪═════╪═══════╡
    #> │ 1   ┆ +   ┆ +   ┆ 2     │
    #> │ 2   ┆ +   ┆ -   ┆ 1     │
    #> │ 3   ┆ -   ┆ +   ┆ 1     │
    #> │ 4   ┆ -   ┆ -   ┆ 1     │
    #> │ 5   ┆ +   ┆ +   ┆ 2     │
    #> └─────┴─────┴─────┴───────┘
