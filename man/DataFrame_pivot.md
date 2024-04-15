

# Pivot data from long to wide

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/dataframe__frame.R#L1566)

## Description

Pivot data from long to wide

## Usage

<pre><code class='language-R'>DataFrame_pivot(
  values,
  index,
  columns,
  ...,
  aggregate_function = NULL,
  maintain_order = TRUE,
  sort_columns = FALSE,
  separator = "_"
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_pivot_:_values">values</code>
</td>
<td>
Column values to aggregate. Can be multiple columns if the
<code>columns</code> arguments contains multiple columns as well.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_pivot_:_index">index</code>
</td>
<td>
One or multiple keys to group by.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_pivot_:_columns">columns</code>
</td>
<td>
Name of the column(s) whose values will be used as the header of the
output DataFrame.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_pivot_:_...">…</code>
</td>
<td>
Not used.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_pivot_:_aggregate_function">aggregate_function</code>
</td>
<td>

One of:

<ul>
<li>

string indicating the expressions to aggregate with, such as ‘first’,
‘sum’, ‘max’, ‘min’, ‘mean’, ‘median’, ‘last’, ‘count’),

</li>
<li>

an Expr e.g. <code>pl$element()$sum()</code>

</li>
</ul>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_pivot_:_maintain_order">maintain_order</code>
</td>
<td>
Sort the grouped keys so that the output order is predictable.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_pivot_:_sort_columns">sort_columns</code>
</td>
<td>
Sort the transposed columns by name. Default is by order of discovery.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_pivot_:_separator">separator</code>
</td>
<td>
Used as separator/delimiter in generated column names.
</td>
</tr>
</table>

## Value

DataFrame

## Examples

``` r
library(polars)

df = pl$DataFrame(
  foo = c("one", "one", "one", "two", "two", "two"),
  bar = c("A", "B", "C", "A", "B", "C"),
  baz = c(1, 2, 3, 4, 5, 6)
)
df
```

    #> shape: (6, 3)
    #> ┌─────┬─────┬─────┐
    #> │ foo ┆ bar ┆ baz │
    #> │ --- ┆ --- ┆ --- │
    #> │ str ┆ str ┆ f64 │
    #> ╞═════╪═════╪═════╡
    #> │ one ┆ A   ┆ 1.0 │
    #> │ one ┆ B   ┆ 2.0 │
    #> │ one ┆ C   ┆ 3.0 │
    #> │ two ┆ A   ┆ 4.0 │
    #> │ two ┆ B   ┆ 5.0 │
    #> │ two ┆ C   ┆ 6.0 │
    #> └─────┴─────┴─────┘

``` r
df$pivot(
  values = "baz", index = "foo", columns = "bar"
)
```

    #> shape: (2, 4)
    #> ┌─────┬─────┬─────┬─────┐
    #> │ foo ┆ A   ┆ B   ┆ C   │
    #> │ --- ┆ --- ┆ --- ┆ --- │
    #> │ str ┆ f64 ┆ f64 ┆ f64 │
    #> ╞═════╪═════╪═════╪═════╡
    #> │ one ┆ 1.0 ┆ 2.0 ┆ 3.0 │
    #> │ two ┆ 4.0 ┆ 5.0 ┆ 6.0 │
    #> └─────┴─────┴─────┴─────┘

``` r
# Run an expression as aggregation function
df = pl$DataFrame(
  col1 = c("a", "a", "a", "b", "b", "b"),
  col2 = c("x", "x", "x", "x", "y", "y"),
  col3 = c(6, 7, 3, 2, 5, 7)
)
df
```

    #> shape: (6, 3)
    #> ┌──────┬──────┬──────┐
    #> │ col1 ┆ col2 ┆ col3 │
    #> │ ---  ┆ ---  ┆ ---  │
    #> │ str  ┆ str  ┆ f64  │
    #> ╞══════╪══════╪══════╡
    #> │ a    ┆ x    ┆ 6.0  │
    #> │ a    ┆ x    ┆ 7.0  │
    #> │ a    ┆ x    ┆ 3.0  │
    #> │ b    ┆ x    ┆ 2.0  │
    #> │ b    ┆ y    ┆ 5.0  │
    #> │ b    ┆ y    ┆ 7.0  │
    #> └──────┴──────┴──────┘

``` r
df$pivot(
  index = "col1",
  columns = "col2",
  values = "col3",
  aggregate_function = pl$element()$tanh()$mean()
)
```

    #> shape: (2, 3)
    #> ┌──────┬──────────┬──────────┐
    #> │ col1 ┆ x        ┆ y        │
    #> │ ---  ┆ ---      ┆ ---      │
    #> │ str  ┆ f64      ┆ f64      │
    #> ╞══════╪══════════╪══════════╡
    #> │ a    ┆ 0.998347 ┆ null     │
    #> │ b    ┆ 0.964028 ┆ 0.999954 │
    #> └──────┴──────────┴──────────┘
