

# Import data in Apache Arrow IPC format

## Description

Import data in Apache Arrow IPC format

## Usage

<pre><code class='language-R'>pl_scan_ipc(
  source,
  ...,
  n_rows = NULL,
  cache = TRUE,
  rechunk = FALSE,
  row_index_name = NULL,
  row_index_offset = 0L,
  memory_map = TRUE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_scan_ipc_:_source">source</code>
</td>
<td>
Path to a file or URL. It is possible to provide multiple paths provided
that all CSV files have the same schema. It is not possible to provide
several URLs.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_scan_ipc_:_...">…</code>
</td>
<td>
Ignored.
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
<code id="pl_scan_ipc_:_row_index_name">row_index_name</code>
</td>
<td>
If not <code>NULL</code>, this will insert a row index column with the
given name into the DataFrame.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_scan_ipc_:_row_index_offset">row_index_offset</code>
</td>
<td>
Offset to start the row index column (only used if the name is set).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_scan_ipc_:_memory_map">memory_map</code>
</td>
<td>
A logical. If <code>TRUE</code>, try to memory map the file. This can
greatly improve performance on repeated queries as the OS may cache
pages. Only uncompressed Arrow IPC files can be memory mapped.
</td>
</tr>
</table>

## Details

Create new LazyFrame from Apache Arrow IPC file or stream

## Value

LazyFrame
