

# Create a arrow RecordBatchReader from a Polars object

## Description

Create a arrow RecordBatchReader from a Polars object

## Usage

<pre><code class='language-R'>## S3 method for class 'RPolarsDataFrame'
as_record_batch_reader(x, ...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_record_batch_reader.RPolarsDataFrame_:_x">x</code>
</td>
<td>
A Polars DataFrame
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_record_batch_reader.RPolarsDataFrame_:_...">…</code>
</td>
<td>
Ignored
</td>
</tr>
</table>

## Examples

``` r
library(polars)

library(arrow)

pl_df = as_polars_df(mtcars)
as_record_batch_reader(pl_df)
```

    #> RecordBatchReader
    #> mpg: double
    #> cyl: double
    #> disp: double
    #> hp: double
    #> drat: double
    #> wt: double
    #> qsec: double
    #> vs: double
    #> am: double
    #> gear: double
    #> carb: double
