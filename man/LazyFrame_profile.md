
# Collect and profile a lazy query.

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L1504)

## Description

This will run the query and return a list containing the materialized
DataFrame and a DataFrame that contains profiling information of each
node that is executed.

## Usage

<pre><code class='language-R'>LazyFrame_profile(
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
  collect_in_background = FALSE,
  show_plot = FALSE,
  truncate_nodes = 0
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_profile_:_type_coercion">type_coercion</code>
</td>
<td>
Boolean. Coerce types such that operations succeed and run on minimal
required memory.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_profile_:_predicate_pushdown">predicate_pushdown</code>
</td>
<td>
Boolean. Applies filters as early as possible at scan level.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_profile_:_projection_pushdown">projection_pushdown</code>
</td>
<td>
Boolean. Select only the columns that are needed at the scan level.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_profile_:_simplify_expression">simplify_expression</code>
</td>
<td>
Boolean. Various optimizations, such as constant folding and replacing
expensive operations with faster alternatives.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_profile_:_slice_pushdown">slice_pushdown</code>
</td>
<td>
Boolean. Only load the required slice from the scan level. Don’t
materialize sliced outputs (e.g. <code>join$head(10)</code>).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_profile_:_comm_subplan_elim">comm_subplan_elim</code>
</td>
<td>
Boolean. Will try to cache branching subplans that occur on self-joins
or unions.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_profile_:_comm_subexpr_elim">comm_subexpr_elim</code>
</td>
<td>
Boolean. Common subexpressions will be cached and reused.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_profile_:_streaming">streaming</code>
</td>
<td>
Boolean. Run parts of the query in a streaming fashion (this is in an
alpha state).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_profile_:_no_optimization">no_optimization</code>
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
<code id="LazyFrame_profile_:_inherit_optimization">inherit_optimization</code>
</td>
<td>
Boolean. Use existing optimization settings regardless the settings
specified in this function call.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_profile_:_collect_in_background">collect_in_background</code>
</td>
<td>
Boolean. Detach this query from R session. Computation will start in
background. Get a handle which later can be converted into the resulting
DataFrame. Useful in interactive mode to not lock R session.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_profile_:_show_plot">show_plot</code>
</td>
<td>
Show a Gantt chart of the profiling result
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_profile_:_truncate_nodes">truncate_nodes</code>
</td>
<td>
Truncate the label lengths in the Gantt chart to this number of
characters. If <code>0</code> (default), do not truncate.
</td>
</tr>
</table>

## Details

The units of the timings are microseconds.

## Value

List of two <code>DataFrame</code>s: one with the collected result, the
other with the timings of each step. If <code>show_graph = TRUE</code>,
then the plot is also stored in the list.

## See Also

<ul>
<li>

<code>$collect()</code> - regular collect.

</li>
<li>

<code>$fetch()</code> - fast limited query check

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

# Simplest use case
pl$LazyFrame()$select(pl$lit(2) + 2)$profile()
```

    #> $result
    #> shape: (1, 1)
    #> ┌─────────┐
    #> │ literal │
    #> │ ---     │
    #> │ f64     │
    #> ╞═════════╡
    #> │ 4.0     │
    #> └─────────┘
    #> 
    #> $profile
    #> shape: (2, 3)
    #> ┌─────────────────────┬───────┬─────┐
    #> │ node                ┆ start ┆ end │
    #> │ ---                 ┆ ---   ┆ --- │
    #> │ str                 ┆ u64   ┆ u64 │
    #> ╞═════════════════════╪═══════╪═════╡
    #> │ optimization        ┆ 0     ┆ 9   │
    #> │ projection(literal) ┆ 9     ┆ 75  │
    #> └─────────────────────┴───────┴─────┘

``` r
# Use $profile() to compare two queries

# -1-  map each Species-group with native polars, takes ~120us only
pl$LazyFrame(iris)$
  sort("Sepal.Length")$
  group_by("Species", maintain_order = TRUE)$
  agg(pl$col(pl$Float64)$first() + 5)$
  profile()
```

    #> $result
    #> shape: (3, 5)
    #> ┌────────────┬──────────────┬─────────────┬──────────────┬─────────────┐
    #> │ Species    ┆ Sepal.Length ┆ Sepal.Width ┆ Petal.Length ┆ Petal.Width │
    #> │ ---        ┆ ---          ┆ ---         ┆ ---          ┆ ---         │
    #> │ cat        ┆ f64          ┆ f64         ┆ f64          ┆ f64         │
    #> ╞════════════╪══════════════╪═════════════╪══════════════╪═════════════╡
    #> │ setosa     ┆ 9.3          ┆ 8.0         ┆ 6.1          ┆ 5.1         │
    #> │ versicolor ┆ 9.9          ┆ 7.4         ┆ 8.3          ┆ 6.0         │
    #> │ virginica  ┆ 9.9          ┆ 7.5         ┆ 9.5          ┆ 6.7         │
    #> └────────────┴──────────────┴─────────────┴──────────────┴─────────────┘
    #> 
    #> $profile
    #> shape: (3, 3)
    #> ┌────────────────────┬───────┬─────┐
    #> │ node               ┆ start ┆ end │
    #> │ ---                ┆ ---   ┆ --- │
    #> │ str                ┆ u64   ┆ u64 │
    #> ╞════════════════════╪═══════╪═════╡
    #> │ optimization       ┆ 0     ┆ 22  │
    #> │ sort(Sepal.Length) ┆ 22    ┆ 516 │
    #> │ group_by(Species)  ┆ 518   ┆ 885 │
    #> └────────────────────┴───────┴─────┘

``` r
# -2-  map each Species-group of each numeric column with an R function, takes ~7000us (slow!)

# some R function, prints `.` for each time called by polars
r_func = \(s) {
  cat(".")
  s$to_r()[1] + 5
}

pl$LazyFrame(iris)$
  sort("Sepal.Length")$
  group_by("Species", maintain_order = TRUE)$
  agg(pl$col(pl$Float64)$map_elements(r_func))$
  profile()
```

    #> ............

    #> $result
    #> shape: (3, 5)
    #> ┌────────────┬────────────────────┬───────────────────┬────────────────────┬───────────────────┐
    #> │ Species    ┆ Sepal.Length_apply ┆ Sepal.Width_apply ┆ Petal.Length_apply ┆ Petal.Width_apply │
    #> │ ---        ┆ ---                ┆ ---               ┆ ---                ┆ ---               │
    #> │ cat        ┆ f64                ┆ f64               ┆ f64                ┆ f64               │
    #> ╞════════════╪════════════════════╪═══════════════════╪════════════════════╪═══════════════════╡
    #> │ setosa     ┆ 9.3                ┆ 8.0               ┆ 6.1                ┆ 5.1               │
    #> │ versicolor ┆ 9.9                ┆ 7.4               ┆ 8.3                ┆ 6.0               │
    #> │ virginica  ┆ 9.9                ┆ 7.5               ┆ 9.5                ┆ 6.7               │
    #> └────────────┴────────────────────┴───────────────────┴────────────────────┴───────────────────┘
    #> 
    #> $profile
    #> shape: (3, 3)
    #> ┌────────────────────┬───────┬───────┐
    #> │ node               ┆ start ┆ end   │
    #> │ ---                ┆ ---   ┆ ---   │
    #> │ str                ┆ u64   ┆ u64   │
    #> ╞════════════════════╪═══════╪═══════╡
    #> │ optimization       ┆ 0     ┆ 6     │
    #> │ sort(Sepal.Length) ┆ 6     ┆ 472   │
    #> │ group_by(Species)  ┆ 474   ┆ 11137 │
    #> └────────────────────┴───────┴───────┘
