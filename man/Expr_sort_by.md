

# Sort Expr by order of others

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L1514)

## Description

Sort this column by the ordering of another column, or multiple other
columns. If used in a groupby context, the groups are sorted.

## Usage

<pre><code class='language-R'>Expr_sort_by(
  by,
  ...,
  descending = FALSE,
  nulls_last = FALSE,
  multithreaded = TRUE,
  maintain_order = FALSE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="by">by</code>
</td>
<td>
One expression or a list of expressions and/or strings (interpreted as
column names).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="descending">descending</code>
</td>
<td>
A logical. If <code>TRUE</code>, sort in descending order.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="nulls_last">nulls_last</code>
</td>
<td>
A logical. If <code>TRUE</code>, place <code>null</code> values last
insead of first.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="multithreaded">multithreaded</code>
</td>
<td>
A logical. If <code>TRUE</code>, sort using multiple threads.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="maintain_order">maintain_order</code>
</td>
<td>
A logical to indicate whether the order should be maintained if elements
are equal.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  group = c("a", "a", "a", "b", "b", "b"),
  value1 = c(98, 1, 3, 2, 99, 100),
  value2 = c("d", "f", "b", "e", "c", "a")
)

# by one column/expression
df$with_columns(
  sorted = pl$col("group")$sort_by("value1")
)
```

    #> shape: (6, 4)
    #> ┌───────┬────────┬────────┬────────┐
    #> │ group ┆ value1 ┆ value2 ┆ sorted │
    #> │ ---   ┆ ---    ┆ ---    ┆ ---    │
    #> │ str   ┆ f64    ┆ str    ┆ str    │
    #> ╞═══════╪════════╪════════╪════════╡
    #> │ a     ┆ 98.0   ┆ d      ┆ a      │
    #> │ a     ┆ 1.0    ┆ f      ┆ b      │
    #> │ a     ┆ 3.0    ┆ b      ┆ a      │
    #> │ b     ┆ 2.0    ┆ e      ┆ a      │
    #> │ b     ┆ 99.0   ┆ c      ┆ b      │
    #> │ b     ┆ 100.0  ┆ a      ┆ b      │
    #> └───────┴────────┴────────┴────────┘

``` r
# by two columns/expressions
df$with_columns(
  sorted = pl$col("group")$sort_by(
    list("value2", pl$col("value1")),
    descending = c(TRUE, FALSE)
  )
)
```

    #> shape: (6, 4)
    #> ┌───────┬────────┬────────┬────────┐
    #> │ group ┆ value1 ┆ value2 ┆ sorted │
    #> │ ---   ┆ ---    ┆ ---    ┆ ---    │
    #> │ str   ┆ f64    ┆ str    ┆ str    │
    #> ╞═══════╪════════╪════════╪════════╡
    #> │ a     ┆ 98.0   ┆ d      ┆ a      │
    #> │ a     ┆ 1.0    ┆ f      ┆ b      │
    #> │ a     ┆ 3.0    ┆ b      ┆ a      │
    #> │ b     ┆ 2.0    ┆ e      ┆ b      │
    #> │ b     ┆ 99.0   ┆ c      ┆ a      │
    #> │ b     ┆ 100.0  ┆ a      ┆ b      │
    #> └───────┴────────┴────────┴────────┘

``` r
# by some expression
df$with_columns(
  sorted = pl$col("group")$sort_by(pl$col("value1")$sort(descending = TRUE))
)
```

    #> shape: (6, 4)
    #> ┌───────┬────────┬────────┬────────┐
    #> │ group ┆ value1 ┆ value2 ┆ sorted │
    #> │ ---   ┆ ---    ┆ ---    ┆ ---    │
    #> │ str   ┆ f64    ┆ str    ┆ str    │
    #> ╞═══════╪════════╪════════╪════════╡
    #> │ a     ┆ 98.0   ┆ d      ┆ b      │
    #> │ a     ┆ 1.0    ┆ f      ┆ b      │
    #> │ a     ┆ 3.0    ┆ b      ┆ b      │
    #> │ b     ┆ 2.0    ┆ e      ┆ a      │
    #> │ b     ┆ 99.0   ┆ c      ┆ a      │
    #> │ b     ┆ 100.0  ┆ a      ┆ a      │
    #> └───────┴────────┴────────┴────────┘
