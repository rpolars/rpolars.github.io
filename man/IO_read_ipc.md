

# Read into a DataFrame from Arrow IPC (Feather v2) file

## Description

Read into a DataFrame from Arrow IPC (Feather v2) file

## Usage

<pre><code class='language-R'>pl_read_ipc(
  source,
  ...,
  n_rows = NULL,
  memory_map = TRUE,
  row_index_name = NULL,
  row_index_offset = 0L,
  rechunk = FALSE,
  cache = TRUE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="source">source</code>
</td>
<td>
Path to a file. You can use globbing with <code>\*</code> to scan/read
multiple files in the same directory (see examples).
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
<code id="n_rows">n_rows</code>
</td>
<td>
Maximum number of rows to read.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="memory_map">memory_map</code>
</td>
<td>
A logical. If <code>TRUE</code>, try to memory map the file. This can
greatly improve performance on repeated queries as the OS may cache
pages. Only uncompressed Arrow IPC files can be memory mapped.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="row_index_name">row_index_name</code>
</td>
<td>
If not <code>NULL</code>, this will insert a row index column with the
given name into the DataFrame.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="row_index_offset">row_index_offset</code>
</td>
<td>
Offset to start the row index column (only used if the name is set).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="rechunk">rechunk</code>
</td>
<td>
In case of reading multiple files via a glob pattern, rechunk the final
DataFrame into contiguous memory chunks.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="cache">cache</code>
</td>
<td>
Cache the result after reading.
</td>
</tr>
</table>

## Value

DataFrame

## Examples

``` r
library(polars)


temp_dir = tempfile()
# Write a hive-style partitioned arrow file dataset
arrow::write_dataset(
  mtcars,
  temp_dir,
  partitioning = c("cyl", "gear"),
  format = "arrow",
  hive_style = TRUE
)
list.files(temp_dir, recursive = TRUE)
```

    #> [1] "cyl=4/gear=3/part-0.arrow" "cyl=4/gear=4/part-0.arrow"
    #> [3] "cyl=4/gear=5/part-0.arrow" "cyl=6/gear=3/part-0.arrow"
    #> [5] "cyl=6/gear=4/part-0.arrow" "cyl=6/gear=5/part-0.arrow"
    #> [7] "cyl=8/gear=3/part-0.arrow" "cyl=8/gear=5/part-0.arrow"

``` r
# Read the dataset
# Sinse hive-style partitioning is not supported,
# the `cyl` and `gear` columns are not contained in the result
pl$read_ipc(
  file.path(temp_dir, "**/*.arrow")
)
```

    #> shape: (32, 9)
    #> ┌──────┬───────┬───────┬──────┬───┬───────┬─────┬─────┬──────┐
    #> │ mpg  ┆ disp  ┆ hp    ┆ drat ┆ … ┆ qsec  ┆ vs  ┆ am  ┆ carb │
    #> │ ---  ┆ ---   ┆ ---   ┆ ---  ┆   ┆ ---   ┆ --- ┆ --- ┆ ---  │
    #> │ f64  ┆ f64   ┆ f64   ┆ f64  ┆   ┆ f64   ┆ f64 ┆ f64 ┆ f64  │
    #> ╞══════╪═══════╪═══════╪══════╪═══╪═══════╪═════╪═════╪══════╡
    #> │ 21.5 ┆ 120.1 ┆ 97.0  ┆ 3.7  ┆ … ┆ 20.01 ┆ 1.0 ┆ 0.0 ┆ 1.0  │
    #> │ 22.8 ┆ 108.0 ┆ 93.0  ┆ 3.85 ┆ … ┆ 18.61 ┆ 1.0 ┆ 1.0 ┆ 1.0  │
    #> │ 24.4 ┆ 146.7 ┆ 62.0  ┆ 3.69 ┆ … ┆ 20.0  ┆ 1.0 ┆ 0.0 ┆ 2.0  │
    #> │ 22.8 ┆ 140.8 ┆ 95.0  ┆ 3.92 ┆ … ┆ 22.9  ┆ 1.0 ┆ 0.0 ┆ 2.0  │
    #> │ 32.4 ┆ 78.7  ┆ 66.0  ┆ 4.08 ┆ … ┆ 19.47 ┆ 1.0 ┆ 1.0 ┆ 1.0  │
    #> │ …    ┆ …     ┆ …     ┆ …    ┆ … ┆ …     ┆ …   ┆ …   ┆ …    │
    #> │ 15.2 ┆ 304.0 ┆ 150.0 ┆ 3.15 ┆ … ┆ 17.3  ┆ 0.0 ┆ 0.0 ┆ 2.0  │
    #> │ 13.3 ┆ 350.0 ┆ 245.0 ┆ 3.73 ┆ … ┆ 15.41 ┆ 0.0 ┆ 0.0 ┆ 4.0  │
    #> │ 19.2 ┆ 400.0 ┆ 175.0 ┆ 3.08 ┆ … ┆ 17.05 ┆ 0.0 ┆ 0.0 ┆ 2.0  │
    #> │ 15.8 ┆ 351.0 ┆ 264.0 ┆ 4.22 ┆ … ┆ 14.5  ┆ 0.0 ┆ 1.0 ┆ 4.0  │
    #> │ 15.0 ┆ 301.0 ┆ 335.0 ┆ 3.54 ┆ … ┆ 14.6  ┆ 0.0 ┆ 1.0 ┆ 8.0  │
    #> └──────┴───────┴───────┴──────┴───┴───────┴─────┴─────┴──────┘
