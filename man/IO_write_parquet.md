

# Write to parquet file

## Description

Write to parquet file

## Usage

<pre><code class='language-R'>DataFrame_write_parquet(
  file,
  ...,
  compression = "zstd",
  compression_level = 3,
  statistics = FALSE,
  row_group_size = NULL,
  data_pagesize_limit = NULL
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_write_parquet_:_file">file</code>
</td>
<td>
File path to which the result should be written.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_write_parquet_:_...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_write_parquet_:_compression">compression</code>
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
<code id="DataFrame_write_parquet_:_compression_level">compression_level</code>
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
<code id="DataFrame_write_parquet_:_statistics">statistics</code>
</td>
<td>
Logical. Whether compute and write column statistics. This requires
extra compute.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_write_parquet_:_row_group_size">row_group_size</code>
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
<code id="DataFrame_write_parquet_:_data_pagesize_limit">data_pagesize_limit</code>
</td>
<td>
<code>NULL</code> or Integer. If <code>NULL</code> (default), the limit
will be ~1MB.
</td>
</tr>
</table>

## Value

This doesn’t return anything.

## Examples

``` r
library(polars)

# write table 'mtcars' from mem to parquet
dat = pl$DataFrame(mtcars)

destination = tempfile(fileext = ".parquet")
dat$write_parquet(destination)
```
