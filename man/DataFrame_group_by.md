
# Group a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L835)

## Description

This doesn’t modify the data but only stores information about the group
structure. This structure can then be used by several functions
(<code style="white-space: pre;">$agg()</code>,
<code style="white-space: pre;">$filter()</code>, etc.).

## Usage

<pre><code class='language-R'>DataFrame_group_by(..., maintain_order = pl\$options\$maintain_order)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_group_by_:_...">…</code>
</td>
<td>
Any Expr(s) or string(s) naming a column.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_group_by_:_maintain_order">maintain_order</code>
</td>
<td>
Keep the same order as the original <code>DataFrame</code>. Setting this
to <code>TRUE</code> makes it more expensive to compute and blocks the
possibility to run on the streaming engine. The default value can be
changed with <code>pl$set_options(maintain_order = TRUE)</code>.
</td>
</tr>
</table>

## Value

GroupBy (a DataFrame with special groupby methods like
<code style="white-space: pre;">$agg()</code>)

## Examples

``` r
library(polars)

gb = pl$DataFrame(
  foo = c("one", "two", "two", "one", "two"),
  bar = c(5, 3, 2, 4, 1)
)$group_by("foo", maintain_order = TRUE)

gb
```

    #> shape: (5, 2)
    #> ┌─────┬─────┐
    #> │ foo ┆ bar │
    #> │ --- ┆ --- │
    #> │ str ┆ f64 │
    #> ╞═════╪═════╡
    #> │ one ┆ 5.0 │
    #> │ two ┆ 3.0 │
    #> │ two ┆ 2.0 │
    #> │ one ┆ 4.0 │
    #> │ two ┆ 1.0 │
    #> └─────┴─────┘
    #> groups: foo
    #> maintain order:  TRUE

``` r
gb$agg(
  pl$col("bar")$sum()$name$suffix("_sum"),
  pl$col("bar")$mean()$alias("bar_tail_sum")
)
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
