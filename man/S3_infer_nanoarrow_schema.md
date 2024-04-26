

# Infer nanoarrow schema from a Polars object

## Description

Infer nanoarrow schema from a Polars object

## Usage

<pre><code class='language-R'>## S3 method for class 'RPolarsDataFrame'
infer_nanoarrow_schema(x, ...)
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

library(nanoarrow)
pl_df = as_polars_df(mtcars)

infer_nanoarrow_schema(pl_df)
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
