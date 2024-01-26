

# New LazyFrame from NDJSON

## Description

Read a file from path into a polars LazyFrame.

## Usage

<pre><code class='language-R'>pl_scan_ndjson(
  path,
  infer_schema_length = 100,
  batch_size = NULL,
  n_rows = NULL,
  low_memory = FALSE,
  rechunk = TRUE,
  row_count_name = NULL,
  row_count_offset = 0,
  reuse_downloaded = TRUE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_scan_ndjson_:_path">path</code>
</td>
<td>
Path to a file or URL. It is possible to provide multiple paths provided
that all NDJSON files have the same schema. It is not possible to
provide several URLs.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_scan_ndjson_:_infer_schema_length">infer_schema_length</code>
</td>
<td>
Maximum number of rows to read to infer the column types. If set to 0,
all columns will be read as UTF-8. If <code>NULL</code>, a full table
scan will be done (slow).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_scan_ndjson_:_batch_size">batch_size</code>
</td>
<td>
Number of rows that will be processed per thread.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_scan_ndjson_:_n_rows">n_rows</code>
</td>
<td>
Maximum number of rows to read.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_scan_ndjson_:_low_memory">low_memory</code>
</td>
<td>
Reduce memory usage (will yield a lower performance).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_scan_ndjson_:_rechunk">rechunk</code>
</td>
<td>
Reallocate to contiguous memory when all chunks / files are parsed.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_scan_ndjson_:_row_count_name">row_count_name</code>
</td>
<td>
If not <code>NULL</code>, this will insert a row count column with the
given name into the DataFrame.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_scan_ndjson_:_row_count_offset">row_count_offset</code>
</td>
<td>
Offset to start the row_count column (only used if the name is set).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_scan_ndjson_:_reuse_downloaded">reuse_downloaded</code>
</td>
<td>
If <code>TRUE</code>(default) and a URL was provided, cache the
downloaded files in session for an easy reuse.
</td>
</tr>
</table>

## Value

A LazyFrame

## Examples

``` r
library(polars)

if (require("jsonlite", quietly = TRUE)) {
  ndjson_filename = tempfile()
  jsonlite::stream_out(iris, file(ndjson_filename), verbose = FALSE)
  pl$scan_ndjson(ndjson_filename)$collect()
}
```

    #> shape: (150, 5)
    #> ┌──────────────┬─────────────┬──────────────┬─────────────┬───────────┐
    #> │ Sepal.Length ┆ Sepal.Width ┆ Petal.Length ┆ Petal.Width ┆ Species   │
    #> │ ---          ┆ ---         ┆ ---          ┆ ---         ┆ ---       │
    #> │ f64          ┆ f64         ┆ f64          ┆ f64         ┆ str       │
    #> ╞══════════════╪═════════════╪══════════════╪═════════════╪═══════════╡
    #> │ 5.1          ┆ 3.5         ┆ 1.4          ┆ 0.2         ┆ setosa    │
    #> │ 4.9          ┆ 3.0         ┆ 1.4          ┆ 0.2         ┆ setosa    │
    #> │ 4.7          ┆ 3.2         ┆ 1.3          ┆ 0.2         ┆ setosa    │
    #> │ 4.6          ┆ 3.1         ┆ 1.5          ┆ 0.2         ┆ setosa    │
    #> │ …            ┆ …           ┆ …            ┆ …           ┆ …         │
    #> │ 6.3          ┆ 2.5         ┆ 5.0          ┆ 1.9         ┆ virginica │
    #> │ 6.5          ┆ 3.0         ┆ 5.2          ┆ 2.0         ┆ virginica │
    #> │ 6.2          ┆ 3.4         ┆ 5.4          ┆ 2.3         ┆ virginica │
    #> │ 5.9          ┆ 3.0         ┆ 5.1          ┆ 1.8         ┆ virginica │
    #> └──────────────┴─────────────┴──────────────┴─────────────┴───────────┘
