

# Fetch <code>n</code> rows of a LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L1448)

## Description

This is similar to <code style="white-space: pre;">$collect()</code> but
limit the number of rows to collect. It is mostly useful to check that a
query works as expected.

## Usage

<pre><code class='language-R'>LazyFrame_fetch(
  n_rows = 500,
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
  inherit_optimization = FALSE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_fetch_:_n_rows">n_rows</code>
</td>
<td>
Integer. Maximum number of rows to fetch.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_fetch_:_...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_fetch_:_type_coercion">type_coercion</code>
</td>
<td>
Boolean. Coerce types such that operations succeed and run on minimal
required memory.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_fetch_:_predicate_pushdown">predicate_pushdown</code>
</td>
<td>
Boolean. Applies filters as early as possible at scan level.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_fetch_:_projection_pushdown">projection_pushdown</code>
</td>
<td>
Boolean. Select only the columns that are needed at the scan level.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_fetch_:_simplify_expression">simplify_expression</code>
</td>
<td>
Boolean. Various optimizations, such as constant folding and replacing
expensive operations with faster alternatives.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_fetch_:_slice_pushdown">slice_pushdown</code>
</td>
<td>
Boolean. Only load the required slice from the scan level. Don’t
materialize sliced outputs (e.g. <code>join$head(10)</code>).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_fetch_:_comm_subplan_elim">comm_subplan_elim</code>
</td>
<td>
Boolean. Will try to cache branching subplans that occur on self-joins
or unions.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_fetch_:_comm_subexpr_elim">comm_subexpr_elim</code>
</td>
<td>
Boolean. Common subexpressions will be cached and reused.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_fetch_:_streaming">streaming</code>
</td>
<td>
Boolean. Run parts of the query in a streaming fashion (this is in an
alpha state).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_fetch_:_no_optimization">no_optimization</code>
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
<code id="LazyFrame_fetch_:_inherit_optimization">inherit_optimization</code>
</td>
<td>
Boolean. Use existing optimization settings regardless the settings
specified in this function call.
</td>
</tr>
</table>

## Details

<code style="white-space: pre;">$fetch()</code> does not guarantee the
final number of rows in the DataFrame output. It only guarantees that
<code>n</code> rows are used at the beginning of the query. Filters,
join operations and a lower number of rows available in the scanned file
influence the final number of rows.

## Value

A DataFrame of maximum n_rows

## See Also

<ul>
<li>

<code>$collect()</code> - regular collect.

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

# fetch 3 rows
pl$LazyFrame(iris)$fetch(3)
```

    #> shape: (3, 5)
    #> ┌──────────────┬─────────────┬──────────────┬─────────────┬─────────┐
    #> │ Sepal.Length ┆ Sepal.Width ┆ Petal.Length ┆ Petal.Width ┆ Species │
    #> │ ---          ┆ ---         ┆ ---          ┆ ---         ┆ ---     │
    #> │ f64          ┆ f64         ┆ f64          ┆ f64         ┆ cat     │
    #> ╞══════════════╪═════════════╪══════════════╪═════════════╪═════════╡
    #> │ 5.1          ┆ 3.5         ┆ 1.4          ┆ 0.2         ┆ setosa  │
    #> │ 4.9          ┆ 3.0         ┆ 1.4          ┆ 0.2         ┆ setosa  │
    #> │ 4.7          ┆ 3.2         ┆ 1.3          ┆ 0.2         ┆ setosa  │
    #> └──────────────┴─────────────┴──────────────┴─────────────┴─────────┘

``` r
# this fetch-query returns 4 rows, because we started with 3 and appended one
# row in the query (see section 'Details')
pl$LazyFrame(iris)$
  select(pl$col("Species")$append("flora gigantica, alien"))$
  fetch(3)
```

    #> shape: (4, 1)
    #> ┌────────────────────────┐
    #> │ Species                │
    #> │ ---                    │
    #> │ str                    │
    #> ╞════════════════════════╡
    #> │ setosa                 │
    #> │ setosa                 │
    #> │ setosa                 │
    #> │ flora gigantica, alien │
    #> └────────────────────────┘
