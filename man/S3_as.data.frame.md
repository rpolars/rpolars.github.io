

# Convert to a data.frame

## Description

Equivalent to <code>as_polars_df(x, …)$to_data_frame(…)</code>.

## Usage

<pre><code class='language-R'>## S3 method for class 'RPolarsDataFrame'
as.data.frame(x, ..., int64_conversion = polars_options()\$int64_conversion)

# S3 method for class 'RPolarsLazyFrame'
as.data.frame(
  x,
  ...,
  n_rows = Inf,
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
<code id="as.data.frame.RPolarsDataFrame_:_x">x</code>
</td>
<td>
An object to convert to a data.frame.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as.data.frame.RPolarsDataFrame_:_...">…</code>
</td>
<td>
Additional arguments passed to methods.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as.data.frame.RPolarsDataFrame_:_int64_conversion">int64_conversion</code>
</td>
<td>

How should Int64 values be handled when converting a polars object to R?

<ul>
<li>

<code>“double”</code> (default) converts the integer values to double.

</li>
<li>

<code>“bit64”</code> uses <code>bit64::as.integer64()</code> to do the
conversion (requires the package <code>bit64</code> to be attached).

</li>
<li>

<code>“string”</code> converts Int64 values to character.

</li>
</ul>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as.data.frame.RPolarsDataFrame_:_n_rows">n_rows</code>
</td>
<td>
Number of rows to fetch. Defaults to <code>Inf</code>, meaning all rows.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as.data.frame.RPolarsDataFrame_:_type_coercion">type_coercion</code>
</td>
<td>
Boolean. Coerce types such that operations succeed and run on minimal
required memory.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as.data.frame.RPolarsDataFrame_:_predicate_pushdown">predicate_pushdown</code>
</td>
<td>
Boolean. Applies filters as early as possible at scan level.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as.data.frame.RPolarsDataFrame_:_projection_pushdown">projection_pushdown</code>
</td>
<td>
Boolean. Select only the columns that are needed at the scan level.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as.data.frame.RPolarsDataFrame_:_simplify_expression">simplify_expression</code>
</td>
<td>
Boolean. Various optimizations, such as constant folding and replacing
expensive operations with faster alternatives.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as.data.frame.RPolarsDataFrame_:_slice_pushdown">slice_pushdown</code>
</td>
<td>
Boolean. Only load the required slice from the scan level. Don’t
materialize sliced outputs (e.g. <code>join$head(10)</code>).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as.data.frame.RPolarsDataFrame_:_comm_subplan_elim">comm_subplan_elim</code>
</td>
<td>
Boolean. Will try to cache branching subplans that occur on self-joins
or unions.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as.data.frame.RPolarsDataFrame_:_comm_subexpr_elim">comm_subexpr_elim</code>
</td>
<td>
Boolean. Common subexpressions will be cached and reused.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as.data.frame.RPolarsDataFrame_:_streaming">streaming</code>
</td>
<td>
Boolean. Run parts of the query in a streaming fashion (this is in an
alpha state).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as.data.frame.RPolarsDataFrame_:_no_optimization">no_optimization</code>
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
<code id="as.data.frame.RPolarsDataFrame_:_inherit_optimization">inherit_optimization</code>
</td>
<td>
Boolean. Use existing optimization settings regardless the settings
specified in this function call.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as.data.frame.RPolarsDataFrame_:_collect_in_background">collect_in_background</code>
</td>
<td>
Boolean. Detach this query from R session. Computation will start in
background. Get a handle which later can be converted into the resulting
DataFrame. Useful in interactive mode to not lock R session.
</td>
</tr>
</table>

## See Also

<ul>
<li>

<code>as_polars_df()</code>

</li>
<li>

<code>\<DataFrame\>$to_data_frame()</code>

</li>
</ul>
