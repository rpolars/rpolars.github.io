
# Collect a query into a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L375)

## Description

<code style="white-space: pre;">$collect()</code> performs the query on
the LazyFrame. It returns a DataFrame

## Usage

<pre><code class='language-R'>LazyFrame_collect(
  ...,
  type_coercion = TRUE,
  predicate_pushdown = TRUE,
  projection_pushdown = TRUE,
  simplify_expression = TRUE,
  slice_pushdown = TRUE,
  comm_subplan_elim = TRUE,
  comm_subexpr_elim = TRUE,
  streaming = FALSE,
  no_optimization = FALSE,
  inherit_optimization = FALSE,
  collect_in_background = FALSE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_collect_:_...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_collect_:_type_coercion">type_coercion</code>
</td>
<td>
Boolean. Coerce types such that operations succeed and run on minimal
required memory.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_collect_:_predicate_pushdown">predicate_pushdown</code>
</td>
<td>
Boolean. Applies filters as early as possible at scan level.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_collect_:_projection_pushdown">projection_pushdown</code>
</td>
<td>
Boolean. Select only the columns that are needed at the scan level.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_collect_:_simplify_expression">simplify_expression</code>
</td>
<td>
Boolean. Various optimizations, such as constant folding and replacing
expensive operations with faster alternatives.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_collect_:_slice_pushdown">slice_pushdown</code>
</td>
<td>
Boolean. Only load the required slice from the scan level. Don’t
materialize sliced outputs (e.g. <code>join$head(10)</code>).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_collect_:_comm_subplan_elim">comm_subplan_elim</code>
</td>
<td>
Boolean. Will try to cache branching subplans that occur on self-joins
or unions.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_collect_:_comm_subexpr_elim">comm_subexpr_elim</code>
</td>
<td>
Boolean. Common subexpressions will be cached and reused.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_collect_:_streaming">streaming</code>
</td>
<td>
Boolean. Run parts of the query in a streaming fashion (this is in an
alpha state).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_collect_:_no_optimization">no_optimization</code>
</td>
<td>
Boolean. Sets the following parameters to <code>FALSE</code>:
<code>predicate_pushdown</code>, <code>projection_pushdown</code>,
<code>slice_pushdown</code>, <code>comm_subplan_elim</code>,
<code>comm_subexpr_elim</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_collect_:_inherit_optimization">inherit_optimization</code>
</td>
<td>
Boolean. Use existing optimization settings regardless the settings
specified in this function call.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_collect_:_collect_in_background">collect_in_background</code>
</td>
<td>
Boolean. Detach this query from R session. Computation will start in
background. Get a handle which later can be converted into the resulting
DataFrame. Useful in interactive mode to not lock R session.
</td>
</tr>
</table>

## Details

Note: use <code style="white-space: pre;">$fetch(n)</code> if you want
to run your query on the first <code>n</code> rows only. This can be a
huge time saver in debugging queries.

## Value

A <code>DataFrame</code>

## See Also

<ul>
<li>

<code>$fetch()</code> - fast limited query check

</li>
<li>

<code>$profile()</code> - same as
<code style="white-space: pre;">$collect()</code> but also returns a
table with each operation profiled.

</li>
<li>

<code>$collect_in_background()</code> - non-blocking collect returns a
future handle. Can also just be used via
<code style="white-space: pre;">$collect(collect_in_background =
TRUE)</code>.

</li>
<li>

<code>$sink_parquet()</code> streams query to a parquet file.

</li>
<li>

<code>$sink_ipc()</code> streams query to a arrow file.

</li>
</ul>

## Examples

``` r
library(polars)

pl$LazyFrame(iris)$filter(pl$col("Species") == "setosa")$collect()
```

    #> shape: (50, 5)
    #> ┌──────────────┬─────────────┬──────────────┬─────────────┬─────────┐
    #> │ Sepal.Length ┆ Sepal.Width ┆ Petal.Length ┆ Petal.Width ┆ Species │
    #> │ ---          ┆ ---         ┆ ---          ┆ ---         ┆ ---     │
    #> │ f64          ┆ f64         ┆ f64          ┆ f64         ┆ cat     │
    #> ╞══════════════╪═════════════╪══════════════╪═════════════╪═════════╡
    #> │ 5.1          ┆ 3.5         ┆ 1.4          ┆ 0.2         ┆ setosa  │
    #> │ 4.9          ┆ 3.0         ┆ 1.4          ┆ 0.2         ┆ setosa  │
    #> │ 4.7          ┆ 3.2         ┆ 1.3          ┆ 0.2         ┆ setosa  │
    #> │ 4.6          ┆ 3.1         ┆ 1.5          ┆ 0.2         ┆ setosa  │
    #> │ …            ┆ …           ┆ …            ┆ …           ┆ …       │
    #> │ 5.1          ┆ 3.8         ┆ 1.6          ┆ 0.2         ┆ setosa  │
    #> │ 4.6          ┆ 3.2         ┆ 1.4          ┆ 0.2         ┆ setosa  │
    #> │ 5.3          ┆ 3.7         ┆ 1.5          ┆ 0.2         ┆ setosa  │
    #> │ 5.0          ┆ 3.3         ┆ 1.4          ┆ 0.2         ┆ setosa  │
    #> └──────────────┴─────────────┴──────────────┴─────────────┴─────────┘
