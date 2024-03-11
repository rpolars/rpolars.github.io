

# Run any polars expression on the list values

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/expr__list.R#L487)

## Description

Run any polars expression on the list values

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
<code>pl$element()</code>, <code>pl$first()</code>, and more. See
Examples.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprList_eval_:_parallel">parallel</code>
</td>
<td>
Run all expression parallel. Don’t activate this blindly. Parallelism is
worth it if there is enough work to do per thread. This likely should
not be used in the <code style="white-space: pre;">$group_by()</code>
context, because we already do parallel execution per group.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = list(c(1, 8, 3), c(3, 2), c(NA, NA, 1)),
  b = list(c("R", "is", "amazing"), c("foo", "bar"), "text")
)

df
```

    #> shape: (3, 2)
    #> ┌───────────────────┬────────────────────────┐
    #> │ a                 ┆ b                      │
    #> │ ---               ┆ ---                    │
    #> │ list[f64]         ┆ list[str]              │
    #> ╞═══════════════════╪════════════════════════╡
    #> │ [1.0, 8.0, 3.0]   ┆ ["R", "is", "amazing"] │
    #> │ [3.0, 2.0]        ┆ ["foo", "bar"]         │
    #> │ [null, null, 1.0] ┆ ["text"]               │
    #> └───────────────────┴────────────────────────┘

``` r
# standardize each value inside a list, using only the values in this list
df$select(
  a_stand = pl$col("a")$list$eval(
    (pl$element() - pl$element()$mean()) / pl$element()$std()
  )
)
```

    #> shape: (3, 1)
    #> ┌──────────────────────────────┐
    #> │ a_stand                      │
    #> │ ---                          │
    #> │ list[f64]                    │
    #> ╞══════════════════════════════╡
    #> │ [-0.83205, 1.1094, -0.27735] │
    #> │ [0.707107, -0.707107]        │
    #> │ [null, null, null]           │
    #> └──────────────────────────────┘

``` r
# count characters for each element in list. Since column "b" is list[str],
# we can apply all `$str` functions on elements in the list:
df$select(
  b_len_chars = pl$col("b")$list$eval(
    pl$element()$str$len_chars()
  )
)
```

    #> shape: (3, 1)
    #> ┌─────────────┐
    #> │ b_len_chars │
    #> │ ---         │
    #> │ list[u32]   │
    #> ╞═════════════╡
    #> │ [1, 2, 7]   │
    #> │ [3, 3]      │
    #> │ [4]         │
    #> └─────────────┘

``` r
# concat strings in each list
df$select(
  pl$col("b")$list$eval(pl$element()$str$concat(" "))$list$first()
)
```

    #> shape: (3, 1)
    #> ┌──────────────┐
    #> │ b            │
    #> │ ---          │
    #> │ str          │
    #> ╞══════════════╡
    #> │ R is amazing │
    #> │ foo bar      │
    #> │ text         │
    #> └──────────────┘
