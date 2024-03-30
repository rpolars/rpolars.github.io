

# Compute expressions over the given groups

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L1863)

## Description

This expression is similar to performing a group by aggregation and
joining the result back into the original DataFrame. The outcome is
similar to how window functions work in
<a href="https://www.postgresql.org/docs/current/tutorial-window.html">PostgreSQL</a>.

## Usage

<pre><code class='language-R'>Expr_over(..., mapping_strategy = "group_to_rows")
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_over_:_...">…</code>
</td>
<td>
Column(s) to group by. Accepts expression input. Characters are parsed
as column names.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_over_:_mapping_strategy">mapping_strategy</code>
</td>
<td>

One of the following:

<ul>
<li>

<code>“group_to_rows”</code> (default): if the aggregation results in
multiple values, assign them back to their position in the DataFrame.
This can only be done if the group yields the same elements before
aggregation as after.

</li>
<li>

<code>“join”</code>: join the groups as
<code style="white-space: pre;">List\<group_dtype\></code> to the row
positions. Note that this can be memory intensive.

</li>
<li>

<code>“explode”</code>: don’t do any mapping, but simply flatten the
group. This only makes sense if the input data is sorted.

</li>
</ul>
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

# Pass the name of a column to compute the expression over that column.
df = pl$DataFrame(
  a = c("a", "a", "b", "b", "b"),
  b = c(1, 2, 3, 5, 3),
  c = c(5, 4, 2, 1, 3)
)

df$with_columns(
  pl$col("c")$max()$over("a")$name$suffix("_max")
)
```

    #> shape: (5, 4)
    #> ┌─────┬─────┬─────┬───────┐
    #> │ a   ┆ b   ┆ c   ┆ c_max │
    #> │ --- ┆ --- ┆ --- ┆ ---   │
    #> │ str ┆ f64 ┆ f64 ┆ f64   │
    #> ╞═════╪═════╪═════╪═══════╡
    #> │ a   ┆ 1.0 ┆ 5.0 ┆ 5.0   │
    #> │ a   ┆ 2.0 ┆ 4.0 ┆ 5.0   │
    #> │ b   ┆ 3.0 ┆ 2.0 ┆ 3.0   │
    #> │ b   ┆ 5.0 ┆ 1.0 ┆ 3.0   │
    #> │ b   ┆ 3.0 ┆ 3.0 ┆ 3.0   │
    #> └─────┴─────┴─────┴───────┘

``` r
# Expression input is supported.
df$with_columns(
  pl$col("c")$max()$over(pl$col("b") %/% 2)$name$suffix("_max")
)
```

    #> shape: (5, 4)
    #> ┌─────┬─────┬─────┬───────┐
    #> │ a   ┆ b   ┆ c   ┆ c_max │
    #> │ --- ┆ --- ┆ --- ┆ ---   │
    #> │ str ┆ f64 ┆ f64 ┆ f64   │
    #> ╞═════╪═════╪═════╪═══════╡
    #> │ a   ┆ 1.0 ┆ 5.0 ┆ 5.0   │
    #> │ a   ┆ 2.0 ┆ 4.0 ┆ 4.0   │
    #> │ b   ┆ 3.0 ┆ 2.0 ┆ 4.0   │
    #> │ b   ┆ 5.0 ┆ 1.0 ┆ 1.0   │
    #> │ b   ┆ 3.0 ┆ 3.0 ┆ 4.0   │
    #> └─────┴─────┴─────┴───────┘

``` r
# Group by multiple columns by passing a character vector of column names
# or list of expressions.
df$with_columns(
  pl$col("c")$min()$over(c("a", "b"))$name$suffix("_min")
)
```

    #> shape: (5, 4)
    #> ┌─────┬─────┬─────┬───────┐
    #> │ a   ┆ b   ┆ c   ┆ c_min │
    #> │ --- ┆ --- ┆ --- ┆ ---   │
    #> │ str ┆ f64 ┆ f64 ┆ f64   │
    #> ╞═════╪═════╪═════╪═══════╡
    #> │ a   ┆ 1.0 ┆ 5.0 ┆ 5.0   │
    #> │ a   ┆ 2.0 ┆ 4.0 ┆ 4.0   │
    #> │ b   ┆ 3.0 ┆ 2.0 ┆ 2.0   │
    #> │ b   ┆ 5.0 ┆ 1.0 ┆ 1.0   │
    #> │ b   ┆ 3.0 ┆ 3.0 ┆ 2.0   │
    #> └─────┴─────┴─────┴───────┘

``` r
df$with_columns(
  pl$col("c")$min()$over(list(pl$col("a"), pl$col("b")))$name$suffix("_min")
)
```

    #> shape: (5, 4)
    #> ┌─────┬─────┬─────┬───────┐
    #> │ a   ┆ b   ┆ c   ┆ c_min │
    #> │ --- ┆ --- ┆ --- ┆ ---   │
    #> │ str ┆ f64 ┆ f64 ┆ f64   │
    #> ╞═════╪═════╪═════╪═══════╡
    #> │ a   ┆ 1.0 ┆ 5.0 ┆ 5.0   │
    #> │ a   ┆ 2.0 ┆ 4.0 ┆ 4.0   │
    #> │ b   ┆ 3.0 ┆ 2.0 ┆ 2.0   │
    #> │ b   ┆ 5.0 ┆ 1.0 ┆ 1.0   │
    #> │ b   ┆ 3.0 ┆ 3.0 ┆ 2.0   │
    #> └─────┴─────┴─────┴───────┘

``` r
# Or use positional arguments to group by multiple columns in the same way.
df$with_columns(
  pl$col("c")$min()$over("a", pl$col("b") %% 2)$name$suffix("_min")
)
```

    #> shape: (5, 4)
    #> ┌─────┬─────┬─────┬───────┐
    #> │ a   ┆ b   ┆ c   ┆ c_min │
    #> │ --- ┆ --- ┆ --- ┆ ---   │
    #> │ str ┆ f64 ┆ f64 ┆ f64   │
    #> ╞═════╪═════╪═════╪═══════╡
    #> │ a   ┆ 1.0 ┆ 5.0 ┆ 5.0   │
    #> │ a   ┆ 2.0 ┆ 4.0 ┆ 4.0   │
    #> │ b   ┆ 3.0 ┆ 2.0 ┆ 1.0   │
    #> │ b   ┆ 5.0 ┆ 1.0 ┆ 1.0   │
    #> │ b   ┆ 3.0 ┆ 3.0 ┆ 1.0   │
    #> └─────┴─────┴─────┴───────┘

``` r
# Alternative mapping strategy: join values in a list output
df$with_columns(
  top_2 = pl$col("c")$top_k(2)$over("a", mapping_strategy = "join")
)
```

    #> shape: (5, 4)
    #> ┌─────┬─────┬─────┬────────────┐
    #> │ a   ┆ b   ┆ c   ┆ top_2      │
    #> │ --- ┆ --- ┆ --- ┆ ---        │
    #> │ str ┆ f64 ┆ f64 ┆ list[f64]  │
    #> ╞═════╪═════╪═════╪════════════╡
    #> │ a   ┆ 1.0 ┆ 5.0 ┆ [5.0, 4.0] │
    #> │ a   ┆ 2.0 ┆ 4.0 ┆ [5.0, 4.0] │
    #> │ b   ┆ 3.0 ┆ 2.0 ┆ [3.0, 2.0] │
    #> │ b   ┆ 5.0 ┆ 1.0 ┆ [3.0, 2.0] │
    #> │ b   ┆ 3.0 ┆ 3.0 ┆ [3.0, 2.0] │
    #> └─────┴─────┴─────┴────────────┘
