

# Group a LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L1134)

## Description

This doesn’t modify the data but only stores information about the group
structure. This structure can then be used by several functions
(<code style="white-space: pre;">$agg()</code>,
<code style="white-space: pre;">$filter()</code>, etc.).

## Usage

<pre><code class='language-R'>LazyFrame_group_by(..., maintain_order = polars_options()\$maintain_order)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_group_by_:_...">…</code>
</td>
<td>
Any Expr(s) or string(s) naming a column.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_group_by_:_maintain_order">maintain_order</code>
</td>
<td>
Keep the same group order as in the original data. Within each group,
the order of rows is always preserved, regardless of this argument.
Setting this to <code>TRUE</code> makes it more expensive to compute and
blocks the possibility to run on the streaming engine. The default value
can be changed with <code>options(polars.maintain_order = TRUE)</code>.
</td>
</tr>
</table>

## Value

LazyGroupBy (a LazyFrame with special groupby methods like
<code style="white-space: pre;">$agg()</code>)

## Examples

``` r
library(polars)

pl$LazyFrame(
  foo = c("one", "two", "two", "one", "two"),
  bar = c(5, 3, 2, 4, 1)
)$
  group_by("foo")$
  agg(
  pl$col("bar")$sum()$name$suffix("_sum"),
  pl$col("bar")$mean()$alias("bar_tail_sum")
)$
  collect()
```

    #> shape: (2, 3)
    #> ┌─────┬─────────┬──────────────┐
    #> │ foo ┆ bar_sum ┆ bar_tail_sum │
    #> │ --- ┆ ---     ┆ ---          │
    #> │ str ┆ f64     ┆ f64          │
    #> ╞═════╪═════════╪══════════════╡
    #> │ one ┆ 9.0     ┆ 4.5          │
    #> │ two ┆ 6.0     ┆ 2.0          │
    #> └─────┴─────────┴──────────────┘
