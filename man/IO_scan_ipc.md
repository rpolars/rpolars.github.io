

# Import data in Apache Arrow IPC format

## Description

Import data in Apache Arrow IPC format

## Usage

<pre><code class='language-R'>pl_scan_ipc(
  path,
  n_rows = NULL,
  cache = TRUE,
  rechunk = TRUE,
  row_count_name = NULL,
  row_count_offset = 0L,
  memmap = TRUE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_scan_ipc_:_path">path</code>
</td>
<td>
Path to a file or URL. It is possible to provide multiple paths provided
that all CSV files have the same schema. It is not possible to provide
several URLs.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_scan_ipc_:_n_rows">n_rows</code>
</td>
<td>
Maximum number of rows to read.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_scan_ipc_:_cache">cache</code>
</td>
<td>
Cache the result after reading.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_scan_ipc_:_rechunk">rechunk</code>
</td>
<td>
Reallocate to contiguous memory when all chunks / files are parsed.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_scan_ipc_:_row_count_name">row_count_name</code>
</td>
<td>
If not <code>NULL</code>, this will insert a row count column with the
given name into the DataFrame.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_scan_ipc_:_row_count_offset">row_count_offset</code>
</td>
<td>
Offset to start the row_count column (only used if the name is set).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_scan_ipc_:_memmap">memmap</code>
</td>
<td>
bool, mapped memory
</td>
</tr>
</table>

## Details

Create new LazyFrame from Apache Arrow IPC file or stream

## Value

LazyFrame
