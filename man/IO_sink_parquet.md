
# Stream the output of a query to a Parquet file

## Description

This writes the output of a query directly to a Parquet file without
collecting it in the R session first. This is useful if the output of
the query is still larger than RAM as it would crash the R session if it
was collected into R.

## Usage

<pre><code class='language-R'>LazyFrame_sink_parquet(
  path,
  compression = "zstd",
  compression_level = 3,
  statistics = FALSE,
  row_group_size = NULL,
  data_pagesize_limit = NULL,
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
<code id="LazyFrame_sink_parquet_:_path">path</code>
</td>
<td>
String. The path of the parquet file
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_sink_parquet_:_compression">compression</code>
</td>
<td>

String. The compression method. One of:

<ul>
<li>

"lz4": fast compression/decompression.

</li>
<li>

"uncompressed"

</li>
<li>

"snappy": this guarantees that the parquet file will be compatible with
older parquet readers.

</li>
<li>

"gzip"

</li>
<li>

"lzo"

</li>
<li>

"brotli"

</li>
<li>

"zstd": good compression performance.

</li>
</ul>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_sink_parquet_:_compression_level">compression_level</code>
</td>
<td>

<code>NULL</code> or Integer. The level of compression to use. Only used
if method is one of ‘gzip’, ‘brotli’, or ‘zstd’. Higher compression
means smaller files on disk:

<ul>
<li>

"gzip": min-level: 0, max-level: 10.

</li>
<li>

"brotli": min-level: 0, max-level: 11.

</li>
<li>

"zstd": min-level: 1, max-level: 22.

</li>
</ul>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_sink_parquet_:_statistics">statistics</code>
</td>
<td>
Boolean. Whether compute and write column statistics. This requires
extra compute.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_sink_parquet_:_row_group_size">row_group_size</code>
</td>
<td>
<code>NULL</code> or Integer. Size of the row groups in number of rows.
If <code>NULL</code> (default), the chunks of the DataFrame are used.
Writing in smaller chunks may reduce memory pressure and improve writing
speeds.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_sink_parquet_:_data_pagesize_limit">data_pagesize_limit</code>
</td>
<td>
<code>NULL</code> or Integer. If <code>NULL</code> (default), the limit
will be ~1MB.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_sink_parquet_:_maintain_order">maintain_order</code>
</td>
<td>
Keep the same order as the original <code>LazyFrame</code>. Setting this
to <code>TRUE</code> makes it more expensive to compute and blocks the
possibility to run on the streaming engine. The default value can be
changed with <code>options(polars.maintain_order = TRUE)</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_sink_parquet_:_type_coercion">type_coercion</code>
</td>
<td>
Boolean. Coerce types such that operations succeed and run on minimal
required memory.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_sink_parquet_:_predicate_pushdown">predicate_pushdown</code>
</td>
<td>
Boolean. Applies filters as early as possible at scan level.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_sink_parquet_:_projection_pushdown">projection_pushdown</code>
</td>
<td>
Boolean. Select only the columns that are needed at the scan level.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_sink_parquet_:_simplify_expression">simplify_expression</code>
</td>
<td>
Boolean. Various optimizations, such as constant folding and replacing
expensive operations with faster alternatives.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_sink_parquet_:_slice_pushdown">slice_pushdown</code>
</td>
<td>
Boolean. Only load the required slice from the scan level. Don’t
materialize sliced outputs (e.g. <code>join$head(10)</code>).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_sink_parquet_:_no_optimization">no_optimization</code>
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
<code id="LazyFrame_sink_parquet_:_inherit_optimization">inherit_optimization</code>
</td>
<td>
Boolean. Use existing optimization settings regardless the settings
specified in this function call.
</td>
</tr>
</table>

## Examples

``` r
library(polars)

# sink table 'mtcars' from mem to parquet
tmpf = tempfile()
pl$LazyFrame(mtcars)$sink_parquet(tmpf)

# stream a query end-to-end
tmpf2 = tempfile()
pl$scan_parquet(tmpf)$select(pl$col("cyl") * 2)$sink_parquet(tmpf2)

# load parquet directly into a DataFrame / memory
pl$scan_parquet(tmpf2)$collect()
```

    #> shape: (32, 1)
    #> ┌──────┐
    #> │ cyl  │
    #> │ ---  │
    #> │ f64  │
    #> ╞══════╡
    #> │ 12.0 │
    #> │ 12.0 │
    #> │ 8.0  │
    #> │ 12.0 │
    #> │ …    │
    #> │ 16.0 │
    #> │ 12.0 │
    #> │ 16.0 │
    #> │ 8.0  │
    #> └──────┘
