

# Combine to a Series

## Description

Combine to a Series

## Usage

<pre><code class='language-R'>## S3 method for class 'RPolarsSeries'
c(x, ...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="c.RPolarsSeries_:_x">x</code>
</td>
<td>
A Polars Series
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="c.RPolarsSeries_:_...">…</code>
</td>
<td>
Series(s) or any object that can be converted to a Series.
</td>
</tr>
</table>

## Details

All objects must have the same datatype. Combining does not rechunk.
Read more about R vectors, Series and chunks in
<code>docs_translations</code>:

## Value

a combined Series

## Examples

``` r
library(polars)

s = c(pl$Series(1:5), 3:1, NA_integer_)
s$chunk_lengths() # the series contain three unmerged chunks
```

    #> [1] 5 3 1
