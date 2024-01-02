
# Initialise a new SQLContext

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/sql.R#L47)

## Description

Create a new SQLContext and register the given LazyFrames.

## Usage

<pre><code class='language-R'>pl_SQLContext(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_SQLContext_:_...">…</code>
</td>
<td>
Name-value pairs of LazyFrame like objects to register.
</td>
</tr>
</table>

## Value

RPolarsSQLContext

## Examples

``` r
library(polars)


ctx = pl$SQLContext(mtcars = mtcars)
ctx
```

    #> RPolarsSQLContext
    #>   tables: mtcars
