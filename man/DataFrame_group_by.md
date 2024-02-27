

# Group a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L866)

## Description

This doesn’t modify the data but only stores information about the group
structure. This structure can then be used by several functions
(<code style="white-space: pre;">$agg()</code>,
<code style="white-space: pre;">$filter()</code>, etc.).

## Usage

<pre><code class='language-R'>DataFrame_group_by(..., maintain_order = polars_options()\$maintain_order)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_group_by_:_...">…</code>
</td>
<td>
Column(s) to group by. Accepts expression input. Characters are parsed
as column names.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_group_by_:_maintain_order">maintain_order</code>
</td>
<td>
Ensure that the order of the groups is consistent with the input data.
This is slower than a default group by. Setting this to
<code>TRUE</code> blocks the possibility to run on the streaming engine.
The default value can be changed with
<code>options(polars.maintain_order = TRUE)</code>.
</td>
</tr>
</table>

## Details

Within each group, the order of the rows is always preserved, regardless
of the <code>maintain_order</code> argument.

## Value

GroupBy (a DataFrame with special groupby methods like
<code style="white-space: pre;">$agg()</code>)

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = c("a", "b", "a", "b", "c"),
  b = c(1, 2, 1, 3, 3),
  c = c(5, 4, 3, 2, 1)
)

df$group_by("a")$agg(pl$col("b")$sum())
```

    #> shape: (3, 2)
    #> ┌─────┬─────┐
    #> │ a   ┆ b   │
    #> │ --- ┆ --- │
    #> │ str ┆ f64 │
    #> ╞═════╪═════╡
    #> │ b   ┆ 5.0 │
    #> │ a   ┆ 2.0 │
    #> │ c   ┆ 3.0 │
    #> └─────┴─────┘

``` r
# Set `maintain_order = TRUE` to ensure the order of the groups is consistent with the input.
df$group_by("a", maintain_order = TRUE)$agg(pl$col("c"))
```

    #> shape: (3, 2)
    #> ┌─────┬────────────┐
    #> │ a   ┆ c          │
    #> │ --- ┆ ---        │
    #> │ str ┆ list[f64]  │
    #> ╞═════╪════════════╡
    #> │ a   ┆ [5.0, 3.0] │
    #> │ b   ┆ [4.0, 2.0] │
    #> │ c   ┆ [1.0]      │
    #> └─────┴────────────┘

``` r
# Group by multiple columns by passing a list of column names.
df$group_by(c("a", "b"))$agg(pl$max("c"))
```

    #> shape: (4, 3)
    #> ┌─────┬─────┬─────┐
    #> │ a   ┆ b   ┆ c   │
    #> │ --- ┆ --- ┆ --- │
    #> │ str ┆ f64 ┆ f64 │
    #> ╞═════╪═════╪═════╡
    #> │ b   ┆ 2.0 ┆ 4.0 │
    #> │ a   ┆ 1.0 ┆ 5.0 │
    #> │ c   ┆ 3.0 ┆ 1.0 │
    #> │ b   ┆ 3.0 ┆ 2.0 │
    #> └─────┴─────┴─────┘

``` r
# Or pass some arguments to group by multiple columns in the same way.
# Expressions are also accepted.
df$group_by("a", pl$col("b") %/% 2)$agg(
  pl$col("c")$mean()
)
```

    #> shape: (3, 3)
    #> ┌─────┬─────┬─────┐
    #> │ a   ┆ b   ┆ c   │
    #> │ --- ┆ --- ┆ --- │
    #> │ str ┆ f64 ┆ f64 │
    #> ╞═════╪═════╪═════╡
    #> │ b   ┆ 1.0 ┆ 3.0 │
    #> │ c   ┆ 1.0 ┆ 1.0 │
    #> │ a   ┆ 0.0 ┆ 4.0 │
    #> └─────┴─────┴─────┘

``` r
# The columns will be renamed to the argument names.
df$group_by(d = "a", e = pl$col("b") %/% 2)$agg(
  pl$col("c")$mean()
)
```

    #> shape: (3, 3)
    #> ┌─────┬─────┬─────┐
    #> │ d   ┆ e   ┆ c   │
    #> │ --- ┆ --- ┆ --- │
    #> │ str ┆ f64 ┆ f64 │
    #> ╞═════╪═════╪═════╡
    #> │ b   ┆ 1.0 ┆ 3.0 │
    #> │ c   ┆ 1.0 ┆ 1.0 │
    #> │ a   ┆ 0.0 ┆ 4.0 │
    #> └─────┴─────┴─────┘
