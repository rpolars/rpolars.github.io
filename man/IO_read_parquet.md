

# Read a parquet file

## Description

Read a parquet file

## Usage

<pre><code class='language-R'>pl_read_parquet(
  file,
  n_rows = NULL,
  cache = TRUE,
  parallel = c("Auto", "None", "Columns", "RowGroups"),
  rechunk = TRUE,
  row_count_name = NULL,
  row_count_offset = 0L,
  low_memory = FALSE,
  use_statistics = TRUE,
  hive_partitioning = TRUE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_read_parquet_:_file">file</code>
</td>
<td>
Path to a file. You can use globbing with <code>\*</code> to scan/read
multiple files in the same directory (see examples).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_read_parquet_:_n_rows">n_rows</code>
</td>
<td>
Maximum number of rows to read.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_read_parquet_:_cache">cache</code>
</td>
<td>
Cache the result after reading.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_read_parquet_:_parallel">parallel</code>
</td>
<td>
This determines the direction of parallelism. <code>“auto”</code> will
try to determine the optimal direction. Can be <code>“auto”</code>,
<code>“none”</code>, <code>“columns”</code>, or
<code>“rowgroups”</code>,
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_read_parquet_:_rechunk">rechunk</code>
</td>
<td>
In case of reading multiple files via a glob pattern, rechunk the final
DataFrame into contiguous memory chunks.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_read_parquet_:_row_count_name">row_count_name</code>
</td>
<td>
If not <code>NULL</code>, this will insert a row count column with the
given name into the DataFrame.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_read_parquet_:_row_count_offset">row_count_offset</code>
</td>
<td>
Offset to start the row_count column (only used if the name is set).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_read_parquet_:_low_memory">low_memory</code>
</td>
<td>
Reduce memory usage (will yield a lower performance).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_read_parquet_:_use_statistics">use_statistics</code>
</td>
<td>
Use statistics in the parquet file to determine if pages can be skipped
from reading.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_read_parquet_:_hive_partitioning">hive_partitioning</code>
</td>
<td>
Infer statistics and schema from hive partitioned URL and use them to
prune reads.
</td>
</tr>
</table>

## Value

DataFrame
