
# Write to JSON file

## Description

Write to JSON file

## Usage

<pre><code class='language-R'>DataFrame_write_json(file, pretty = FALSE, row_oriented = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_write_json_:_file">file</code>
</td>
<td>
File path to which the result should be written.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_write_json_:_pretty">pretty</code>
</td>
<td>
Pretty serialize JSON.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_write_json_:_row_oriented">row_oriented</code>
</td>
<td>
Write to row-oriented JSON. This is slower, but more common.
</td>
</tr>
</table>

## Value

This doesn’t return anything.

## Examples

``` r
library(polars)

if (require("jsonlite", quiet = TRUE)) {
  dat = pl$DataFrame(head(mtcars))
  destination = tempfile()

  dat$select(pl$col("drat", "mpg"))$write_json(destination)
  jsonlite::fromJSON(destination)

  dat$select(pl$col("drat", "mpg"))$write_json(destination, row_oriented = TRUE)
  jsonlite::fromJSON(destination)
}
```

    #>   drat  mpg
    #> 1 3.90 21.0
    #> 2 3.90 21.0
    #> 3 3.85 22.8
    #> 4 3.08 21.4
    #> 5 3.15 18.7
    #> 6 2.76 18.1
