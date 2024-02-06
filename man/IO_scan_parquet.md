

# Scan a parquet file

## Description

Scan a parquet file

## Usage

<pre><code class='language-R'>pl_scan_parquet(
  file,
  n_rows = NULL,
  cache = TRUE,
  parallel = c("Auto", "None", "Columns", "RowGroups"),
  rechunk = TRUE,
  row_index_name = NULL,
  row_index_offset = 0L,
  low_memory = FALSE,
  use_statistics = TRUE,
  hive_partitioning = TRUE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="scan_parquet_:_file">file</code>
</td>
<td>
Path to a file. You can use globbing with <code>\*</code> to scan/read
multiple files in the same directory (see examples).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="scan_parquet_:_n_rows">n_rows</code>
</td>
<td>
Maximum number of rows to read.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="scan_parquet_:_cache">cache</code>
</td>
<td>
Cache the result after reading.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="scan_parquet_:_parallel">parallel</code>
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
<code id="scan_parquet_:_rechunk">rechunk</code>
</td>
<td>
In case of reading multiple files via a glob pattern, rechunk the final
DataFrame into contiguous memory chunks.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="scan_parquet_:_row_index_name">row_index_name</code>
</td>
<td>
If not <code>NULL</code>, this will insert a row count column with the
given name into the DataFrame.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="scan_parquet_:_row_index_offset">row_index_offset</code>
</td>
<td>
Offset to start the row_index column (only used if the name is set).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="scan_parquet_:_low_memory">low_memory</code>
</td>
<td>
Reduce memory usage (will yield a lower performance).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="scan_parquet_:_use_statistics">use_statistics</code>
</td>
<td>
Use statistics in the parquet file to determine if pages can be skipped
from reading.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="scan_parquet_:_hive_partitioning">hive_partitioning</code>
</td>
<td>
Infer statistics and schema from hive partitioned URL and use them to
prune reads.
</td>
</tr>
</table>

## Value

LazyFrame

## Examples

``` r
library(polars)


temp_dir = tempfile()
# Write a hive-style partitioned parquet dataset
arrow::write_dataset(
  mtcars,
  temp_dir,
  partitioning = c("cyl", "gear"),
  format = "parquet",
  hive_style = TRUE
)
list.files(temp_dir, recursive = TRUE)
```

    #> [1] "cyl=4/gear=3/part-0.parquet" "cyl=4/gear=4/part-0.parquet"
    #> [3] "cyl=4/gear=5/part-0.parquet" "cyl=6/gear=3/part-0.parquet"
    #> [5] "cyl=6/gear=4/part-0.parquet" "cyl=6/gear=5/part-0.parquet"
    #> [7] "cyl=8/gear=3/part-0.parquet" "cyl=8/gear=5/part-0.parquet"

``` r
# Read the dataset
pl$scan_parquet(
  file.path(temp_dir, "**/*.parquet")
)$collect()
```

    #> shape: (32, 11)
    #> ┌──────┬───────┬───────┬──────┬───┬─────┬──────┬─────┬──────┐
    #> │ mpg  ┆ disp  ┆ hp    ┆ drat ┆ … ┆ am  ┆ carb ┆ cyl ┆ gear │
    #> │ ---  ┆ ---   ┆ ---   ┆ ---  ┆   ┆ --- ┆ ---  ┆ --- ┆ ---  │
    #> │ f64  ┆ f64   ┆ f64   ┆ f64  ┆   ┆ f64 ┆ f64  ┆ i64 ┆ i64  │
    #> ╞══════╪═══════╪═══════╪══════╪═══╪═════╪══════╪═════╪══════╡
    #> │ 21.5 ┆ 120.1 ┆ 97.0  ┆ 3.7  ┆ … ┆ 0.0 ┆ 1.0  ┆ 4   ┆ 3    │
    #> │ 22.8 ┆ 108.0 ┆ 93.0  ┆ 3.85 ┆ … ┆ 1.0 ┆ 1.0  ┆ 4   ┆ 4    │
    #> │ 24.4 ┆ 146.7 ┆ 62.0  ┆ 3.69 ┆ … ┆ 0.0 ┆ 2.0  ┆ 4   ┆ 4    │
    #> │ 22.8 ┆ 140.8 ┆ 95.0  ┆ 3.92 ┆ … ┆ 0.0 ┆ 2.0  ┆ 4   ┆ 4    │
    #> │ 32.4 ┆ 78.7  ┆ 66.0  ┆ 4.08 ┆ … ┆ 1.0 ┆ 1.0  ┆ 4   ┆ 4    │
    #> │ …    ┆ …     ┆ …     ┆ …    ┆ … ┆ …   ┆ …    ┆ …   ┆ …    │
    #> │ 15.2 ┆ 304.0 ┆ 150.0 ┆ 3.15 ┆ … ┆ 0.0 ┆ 2.0  ┆ 8   ┆ 3    │
    #> │ 13.3 ┆ 350.0 ┆ 245.0 ┆ 3.73 ┆ … ┆ 0.0 ┆ 4.0  ┆ 8   ┆ 3    │
    #> │ 19.2 ┆ 400.0 ┆ 175.0 ┆ 3.08 ┆ … ┆ 0.0 ┆ 2.0  ┆ 8   ┆ 3    │
    #> │ 15.8 ┆ 351.0 ┆ 264.0 ┆ 4.22 ┆ … ┆ 1.0 ┆ 4.0  ┆ 8   ┆ 5    │
    #> │ 15.0 ┆ 301.0 ┆ 335.0 ┆ 3.54 ┆ … ┆ 1.0 ┆ 8.0  ┆ 8   ┆ 5    │
    #> └──────┴───────┴───────┴──────┴───┴─────┴──────┴─────┴──────┘
