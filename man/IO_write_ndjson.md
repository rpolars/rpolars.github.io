

# Write to NDJSON file

## Description

Write to NDJSON file

## Usage

<pre><code class='language-R'>DataFrame_write_ndjson(file)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_write_ndjson_:_file">file</code>
</td>
<td>
File path to which the result should be written.
</td>
</tr>
</table>

## Value

This doesn’t return anything.

## Examples

``` r
library(polars)

dat = pl$DataFrame(head(mtcars))

destination = tempfile()
dat$select(pl$col("drat", "mpg"))$write_ndjson(destination)

pl$read_ndjson(destination)
```

    #> shape: (6, 2)
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
    #> │ 2.76 ┆ 18.1 │
    #> └──────┴──────┘
