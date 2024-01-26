

# polars to nanoarrow and arrow

## Description

Conversion via native apache arrow array stream (fast), THIS REQUIRES
´nanoarrow´

## Usage

<pre><code class='language-R'>## S3 method for class 'RPolarsDataFrame'
as_nanoarrow_array_stream(x, ..., schema = NULL)

# S3 method for class 'RPolarsDataFrame'
infer_nanoarrow_schema(x, ...)

# S3 method for class 'RPolarsDataFrame'
as_arrow_table(x, ...)

# S3 method for class 'RPolarsDataFrame'
as_record_batch_reader(x, ..., schema = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="nanoarrow_:_x">x</code>
</td>
<td>
a polars DataFrame
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="nanoarrow_:_...">…</code>
</td>
<td>
not used right now
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="nanoarrow_:_schema">schema</code>
</td>
<td>
must stay at default value NULL
</td>
</tr>
</table>

## Details

The following functions enable conversion to <code>nanoarrow</code> and
<code>arrow</code>. Conversion kindly provided by "paleolimbot / Dewey
Dunnington" Author of <code>nanoarrow</code>. Currently these
conversions are the fastest way to convert from polars to R.

## Value

<ul>
<li>

a nanoarrow array stream

</li>
</ul>
<ul>
<li>

a nanoarrow array schema

</li>
</ul>
<ul>
<li>

an arrow table

</li>
</ul>
<ul>
<li>

an arrow record batch reader

</li>
</ul>

## Examples

``` r
library(polars)

library(nanoarrow)
df = pl$DataFrame(mtcars)
nanoarrow_array_stream = as_nanoarrow_array_stream(df)
rdf = as.data.frame(nanoarrow_array_stream)
print(head(rdf))
```

    #>    mpg cyl disp  hp drat    wt  qsec vs am gear carb
    #> 1 21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
    #> 2 21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
    #> 3 22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
    #> 4 21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
    #> 5 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
    #> 6 18.1   6  225 105 2.76 3.460 20.22  1  0    3    1

``` r
nanoarrow_array_schema = infer_nanoarrow_schema(df)
print(nanoarrow_array_schema)
```

    #> <nanoarrow_schema struct>
    #>  $ format    : chr "+s"
    #>  $ name      : chr ""
    #>  $ metadata  : list()
    #>  $ flags     : int 0
    #>  $ children  :List of 11
    #>   ..$ mpg :<nanoarrow_schema double>
    #>   .. ..$ format    : chr "g"
    #>   .. ..$ name      : chr "mpg"
    #>   .. ..$ metadata  : list()
    #>   .. ..$ flags     : int 2
    #>   .. ..$ children  : list()
    #>   .. ..$ dictionary: NULL
    #>   ..$ cyl :<nanoarrow_schema double>
    #>   .. ..$ format    : chr "g"
    #>   .. ..$ name      : chr "cyl"
    #>   .. ..$ metadata  : list()
    #>   .. ..$ flags     : int 2
    #>   .. ..$ children  : list()
    #>   .. ..$ dictionary: NULL
    #>   ..$ disp:<nanoarrow_schema double>
    #>   .. ..$ format    : chr "g"
    #>   .. ..$ name      : chr "disp"
    #>   .. ..$ metadata  : list()
    #>   .. ..$ flags     : int 2
    #>   .. ..$ children  : list()
    #>   .. ..$ dictionary: NULL
    #>   ..$ hp  :<nanoarrow_schema double>
    #>   .. ..$ format    : chr "g"
    #>   .. ..$ name      : chr "hp"
    #>   .. ..$ metadata  : list()
    #>   .. ..$ flags     : int 2
    #>   .. ..$ children  : list()
    #>   .. ..$ dictionary: NULL
    #>   ..$ drat:<nanoarrow_schema double>
    #>   .. ..$ format    : chr "g"
    #>   .. ..$ name      : chr "drat"
    #>   .. ..$ metadata  : list()
    #>   .. ..$ flags     : int 2
    #>   .. ..$ children  : list()
    #>   .. ..$ dictionary: NULL
    #>   ..$ wt  :<nanoarrow_schema double>
    #>   .. ..$ format    : chr "g"
    #>   .. ..$ name      : chr "wt"
    #>   .. ..$ metadata  : list()
    #>   .. ..$ flags     : int 2
    #>   .. ..$ children  : list()
    #>   .. ..$ dictionary: NULL
    #>   ..$ qsec:<nanoarrow_schema double>
    #>   .. ..$ format    : chr "g"
    #>   .. ..$ name      : chr "qsec"
    #>   .. ..$ metadata  : list()
    #>   .. ..$ flags     : int 2
    #>   .. ..$ children  : list()
    #>   .. ..$ dictionary: NULL
    #>   ..$ vs  :<nanoarrow_schema double>
    #>   .. ..$ format    : chr "g"
    #>   .. ..$ name      : chr "vs"
    #>   .. ..$ metadata  : list()
    #>   .. ..$ flags     : int 2
    #>   .. ..$ children  : list()
    #>   .. ..$ dictionary: NULL
    #>   ..$ am  :<nanoarrow_schema double>
    #>   .. ..$ format    : chr "g"
    #>   .. ..$ name      : chr "am"
    #>   .. ..$ metadata  : list()
    #>   .. ..$ flags     : int 2
    #>   .. ..$ children  : list()
    #>   .. ..$ dictionary: NULL
    #>   ..$ gear:<nanoarrow_schema double>
    #>   .. ..$ format    : chr "g"
    #>   .. ..$ name      : chr "gear"
    #>   .. ..$ metadata  : list()
    #>   .. ..$ flags     : int 2
    #>   .. ..$ children  : list()
    #>   .. ..$ dictionary: NULL
    #>   ..$ carb:<nanoarrow_schema double>
    #>   .. ..$ format    : chr "g"
    #>   .. ..$ name      : chr "carb"
    #>   .. ..$ metadata  : list()
    #>   .. ..$ flags     : int 2
    #>   .. ..$ children  : list()
    #>   .. ..$ dictionary: NULL
    #>  $ dictionary: NULL

``` r
library(arrow)
arrow_table = as_arrow_table(df)
print(arrow_table)
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

``` r
arrow_record_batch_reader = as_record_batch_reader(df) # requires arrow
print(arrow_record_batch_reader)
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
