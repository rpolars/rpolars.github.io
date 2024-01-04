
# eval sublists (kinda like lapply)

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__list.R#L421)

## Description

Run any polars expression against the lists’ elements.

## Usage

<pre><code class='language-R'>ExprList_eval(expr, parallel = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_eval_:_expr">expr</code>
</td>
<td>
Expression to run. Note that you can select an element with
<code>pl$first()</code>, or <code>pl$col()</code>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_eval_:_parallel">parallel</code>
</td>
<td>
Run all expression parallel. Don’t activate this blindly. Parallelism is
worth it if there is enough work to do per thread. This likely should
not be use in the groupby context, because we already do parallel
execution per group.
</td>
</tr>
</table>

## Format

function

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(a = c(1, 8, 3), b = c(4, 5, 2))
df$select(pl$all()$cast(pl$dtypes$Int64))$with_columns(
  pl$concat_list(c("a", "b"))$list$eval(pl$element()$rank())$alias("rank")
)
```

    #> shape: (3, 3)
    #> ┌─────┬─────┬────────────┐
    #> │ a   ┆ b   ┆ rank       │
    #> │ --- ┆ --- ┆ ---        │
    #> │ i64 ┆ i64 ┆ list[f64]  │
    #> ╞═════╪═════╪════════════╡
    #> │ 1   ┆ 4   ┆ [1.0, 2.0] │
    #> │ 8   ┆ 5   ┆ [2.0, 1.0] │
    #> │ 3   ┆ 2   ┆ [2.0, 1.0] │
    #> └─────┴─────┴────────────┘
