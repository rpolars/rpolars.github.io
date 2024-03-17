

# Stream the output of a query to an Arrow IPC file

## Description

This writes the output of a query directly to an Arrow IPC file without
collecting it in the R session first. This is useful if the output of
the query is still larger than RAM as it would crash the R session if it
was collected into R.

## Usage

<pre><code class='language-R'>LazyFrame_sink_ipc(
  path,
  compression = "zstd",
  maintain_order = TRUE,
  type_coercion = TRUE,
  predicate_pushdown = TRUE,
  projection_pushdown = TRUE,
  simplify_expression = TRUE,
  slice_pushdown = TRUE,
  no_optimization = FALSE,
  inherit_optimization = FALSE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_sink_ipc_:_path">path</code>
</td>
<td>
String. The path to the Arrow IPC file
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_sink_ipc_:_compression">compression</code>
</td>
<td>
<code>NULL</code> or string, the compression method. One of
<code>NULL</code>, "lz4" or "zstd". Choose "zstd" for good compression
performance. Choose "lz4" for fast compression/decompression.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_sink_ipc_:_maintain_order">maintain_order</code>
</td>
<td>
Maintain the order in which data is processed. Setting this to
<code>FALSE</code> will be slightly faster.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_sink_ipc_:_type_coercion">type_coercion</code>
</td>
<td>
Logical. Coerce types such that operations succeed and run on minimal
required memory.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_sink_ipc_:_predicate_pushdown">predicate_pushdown</code>
</td>
<td>
Logical. Applies filters as early as possible at scan level.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_sink_ipc_:_projection_pushdown">projection_pushdown</code>
</td>
<td>
Logical. Select only the columns that are needed at the scan level.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_sink_ipc_:_simplify_expression">simplify_expression</code>
</td>
<td>
Logical. Various optimizations, such as constant folding and replacing
expensive operations with faster alternatives.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_sink_ipc_:_slice_pushdown">slice_pushdown</code>
</td>
<td>
Logical. Only load the required slice from the scan level. Don’t
materialize sliced outputs (e.g. <code>join$head(10)</code>).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_sink_ipc_:_no_optimization">no_optimization</code>
</td>
<td>
Logical. Sets the following parameters to <code>FALSE</code>:
<code>predicate_pushdown</code>, <code>projection_pushdown</code>,
<code>slice_pushdown</code>, <code>comm_subplan_elim</code>,
<code>comm_subexpr_elim</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_sink_ipc_:_inherit_optimization">inherit_optimization</code>
</td>
<td>
Logical. Use existing optimization settings regardless the settings
specified in this function call.
</td>
</tr>
</table>

## Examples

``` r
library(polars)

# sink table 'mtcars' from mem to ipc
tmpf = tempfile()
pl$LazyFrame(mtcars)$sink_ipc(tmpf)

# stream a query end-to-end (not supported yet, https://github.com/pola-rs/polars/issues/1040)
# tmpf2 = tempfile()
# pl$scan_ipc(tmpf)$select(pl$col("cyl") * 2)$sink_ipc(tmpf2)

# load ipc directly into a DataFrame / memory
# pl$scan_ipc(tmpf2)$collect()
```
