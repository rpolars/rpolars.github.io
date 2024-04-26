

# Stream the output of a query to a CSV file

## Description

This writes the output of a query directly to a CSV file without
collecting it in the R session first. This is useful if the output of
the query is still larger than RAM as it would crash the R session if it
was collected into R.

## Usage

<pre><code class='language-R'>LazyFrame_sink_csv(
  path,
  ...,
  include_bom = FALSE,
  include_header = TRUE,
  separator = ",",
  line_terminator = "\n",
  quote = "\"",
  batch_size = 1024,
  datetime_format = NULL,
  date_format = NULL,
  time_format = NULL,
  float_precision = NULL,
  null_values = "",
  quote_style = "necessary",
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
<code id="path">path</code>
</td>
<td>
A character. File path to which the file should be written.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="include_bom">include_bom</code>
</td>
<td>
Whether to include UTF-8 BOM (byte order mark) in the CSV output.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="include_header">include_header</code>
</td>
<td>
Whether to include header in the CSV output.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="separator">separator</code>
</td>
<td>
Separate CSV fields with this symbol.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="line_terminator">line_terminator</code>
</td>
<td>
String used to end each row.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="quote">quote</code>
</td>
<td>
Byte to use as quoting character.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="batch_size">batch_size</code>
</td>
<td>
Number of rows that will be processed per thread.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="datetime_format">datetime_format</code>
</td>
<td>
A format string, with the specifiers defined by the chrono Rust crate.
If no format specified, the default fractional-second precision is
inferred from the maximum timeunit found in the frame’s Datetime cols
(if any).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="date_format">date_format</code>
</td>
<td>
A format string, with the specifiers defined by the chrono Rust crate.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="time_format">time_format</code>
</td>
<td>
A format string, with the specifiers defined by the chrono Rust crate.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="float_precision">float_precision</code>
</td>
<td>
Number of decimal places to write, applied to both Float32 and Float64
datatypes.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="null_values">null_values</code>
</td>
<td>
A string representing null values (defaulting to the empty string).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="quote_style">quote_style</code>
</td>
<td>

Determines the quoting strategy used.

<ul>
<li>

<code>“necessary”</code> (default): This puts quotes around fields only
when necessary. They are necessary when fields contain a quote,
delimiter or record terminator. Quotes are also necessary when writing
an empty record (which is indistinguishable from a record with one empty
field). This is the default.

</li>
<li>

<code>“always”</code>: This puts quotes around every field.

</li>
<li>

<code>“non_numeric”</code>: This puts quotes around all fields that are
non-numeric. Namely, when writing a field that does not parse as a valid
float or integer, then quotes will be used even if they aren’t strictly
necessary.

</li>
<li>

<code>“never”</code>: This never puts quotes around fields, even if that
results in invalid CSV data (e.g. by not quoting strings containing the
separator).

</li>
</ul>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="maintain_order">maintain_order</code>
</td>
<td>
Maintain the order in which data is processed. Setting this to
<code>FALSE</code> will be slightly faster.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="type_coercion">type_coercion</code>
</td>
<td>
Logical. Coerce types such that operations succeed and run on minimal
required memory.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="predicate_pushdown">predicate_pushdown</code>
</td>
<td>
Logical. Applies filters as early as possible at scan level.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="projection_pushdown">projection_pushdown</code>
</td>
<td>
Logical. Select only the columns that are needed at the scan level.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="simplify_expression">simplify_expression</code>
</td>
<td>
Logical. Various optimizations, such as constant folding and replacing
expensive operations with faster alternatives.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="slice_pushdown">slice_pushdown</code>
</td>
<td>
Logical. Only load the required slice from the scan level. Don’t
materialize sliced outputs (e.g. <code>join$head(10)</code>).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="no_optimization">no_optimization</code>
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
<code id="inherit_optimization">inherit_optimization</code>
</td>
<td>
Logical. Use existing optimization settings regardless the settings
specified in this function call.
</td>
</tr>
</table>

## Value

Invisibly returns the input LazyFrame

## Examples

``` r
library(polars)

# sink table 'mtcars' from mem to CSV
tmpf = tempfile()
pl$LazyFrame(mtcars)$sink_csv(tmpf)

# stream a query end-to-end
tmpf2 = tempfile()
pl$scan_csv(tmpf)$select(pl$col("cyl") * 2)$sink_csv(tmpf2)

# load parquet directly into a DataFrame / memory
pl$scan_csv(tmpf2)$collect()
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
    #> │ 16.0 │
    #> │ …    │
    #> │ 8.0  │
    #> │ 16.0 │
    #> │ 12.0 │
    #> │ 16.0 │
    #> │ 8.0  │
    #> └──────┘
