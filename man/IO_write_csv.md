

# Write to comma-separated values (CSV) file

## Description

Write to comma-separated values (CSV) file

## Usage

<pre><code class='language-R'>DataFrame_write_csv(
  file,
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
  quote_style = "necessary"
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_write_csv_:_file">file</code>
</td>
<td>
File path to which the result should be written.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_write_csv_:_...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_write_csv_:_include_bom">include_bom</code>
</td>
<td>
Whether to include UTF-8 BOM (byte order mark) in the CSV output.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_write_csv_:_include_header">include_header</code>
</td>
<td>
Whether to include header in the CSV output.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_write_csv_:_separator">separator</code>
</td>
<td>
Separate CSV fields with this symbol.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_write_csv_:_line_terminator">line_terminator</code>
</td>
<td>
String used to end each row.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_write_csv_:_quote">quote</code>
</td>
<td>
Byte to use as quoting character.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_write_csv_:_batch_size">batch_size</code>
</td>
<td>
Number of rows that will be processed per thread.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_write_csv_:_datetime_format">datetime_format</code>
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
<code id="DataFrame_write_csv_:_date_format">date_format</code>
</td>
<td>
A format string, with the specifiers defined by the chrono Rust crate.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_write_csv_:_time_format">time_format</code>
</td>
<td>
A format string, with the specifiers defined by the chrono Rust crate.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_write_csv_:_float_precision">float_precision</code>
</td>
<td>
Number of decimal places to write, applied to both Float32 and Float64
datatypes.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_write_csv_:_null_values">null_values</code>
</td>
<td>
A string representing null values (defaulting to the empty string).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_write_csv_:_quote_style">quote_style</code>
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
</table>

## Value

This doesn’t return anything but creates a CSV file.

## Examples

``` r
library(polars)

dat = pl$DataFrame(mtcars)

destination = tempfile(fileext = ".csv")
dat$select(pl$col("drat", "mpg"))$write_csv(destination)

pl$read_csv(destination)
```

    #> shape: (32, 2)
    #> ┌──────┬──────┐
    #> │ drat ┆ mpg  │
    #> │ ---  ┆ ---  │
    #> │ f64  ┆ f64  │
    #> ╞══════╪══════╡
    #> │ 3.9  ┆ 21.0 │
    #> │ 3.9  ┆ 21.0 │
    #> │ 3.85 ┆ 22.8 │
    #> │ 3.08 ┆ 21.4 │
    #> │ 3.15 ┆ 18.7 │
    #> │ …    ┆ …    │
    #> │ 3.77 ┆ 30.4 │
    #> │ 4.22 ┆ 15.8 │
    #> │ 3.62 ┆ 19.7 │
    #> │ 3.54 ┆ 15.0 │
    #> │ 4.11 ┆ 21.4 │
    #> └──────┴──────┘
