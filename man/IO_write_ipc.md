

# Write to Arrow IPC file (a.k.a Feather file)

## Description

Write to Arrow IPC file (a.k.a Feather file)

## Usage

<pre><code class='language-R'>DataFrame_write_ipc(
  file,
  compression = c("uncompressed", "zstd", "lz4"),
  ...,
  future = FALSE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="file">file</code>
</td>
<td>
File path to which the result should be written.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="compression">compression</code>
</td>
<td>
<code>NULL</code> or a character of the compression method,
<code>“uncompressed”</code> or "lz4" or "zstd". <code>NULL</code> is
equivalent to <code>“uncompressed”</code>. Choose "zstd" for good
compression performance. Choose "lz4" for fast
compression/decompression.
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
<code id="future">future</code>
</td>
<td>
Setting this to <code>TRUE</code> will write Polars’ internal data
structures that might not be available by other Arrow implementations.
This functionality is considered <strong>unstable</strong>. It may be
changed at any point without it being considered a breaking change.
</td>
</tr>
</table>

## Value

Invisibly returns the input DataFrame.

## Examples

``` r
library(polars)

dat = pl$DataFrame(mtcars)

destination = tempfile(fileext = ".arrow")
dat$write_ipc(destination)

if (require("arrow", quietly = TRUE)) {
  arrow::read_ipc_file(destination, as_data_frame = FALSE)
}
```

    #> Table
    #> 32 rows x 11 columns
    #> $mpg <double>
    #> $cyl <double>
    #> $disp <double>
    #> $hp <double>
    #> $drat <double>
    #> $wt <double>
    #> $qsec <double>
    #> $vs <double>
    #> $am <double>
    #> $gear <double>
    #> $carb <double>
