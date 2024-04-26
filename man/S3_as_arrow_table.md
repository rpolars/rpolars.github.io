

# Create a arrow Table from a Polars object

## Description

Create a arrow Table from a Polars object

## Usage

<pre><code class='language-R'>## S3 method for class 'RPolarsDataFrame'
as_arrow_table(x, ...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="x">x</code>
</td>
<td>
A Polars DataFrame
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="...">…</code>
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
as_arrow_table(pl_df)
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
