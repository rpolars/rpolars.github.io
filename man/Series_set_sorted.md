

# Set a sorted flag on a Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/series__series.R#L889)

## Description

Set a sorted flag on a Series

## Usage

<pre><code class='language-R'>Series_set_sorted(..., descending = FALSE, in_place = FALSE)
</code></pre>

## Arguments

<table>
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
<code id="descending">descending</code>
</td>
<td>
Sort the columns in descending order.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="in_place">in_place</code>
</td>
<td>
If <code>TRUE</code>, this will set the flag mutably and return
<code>NULL</code>. Remember to use
<code>options(polars.strictly_immutable = FALSE)</code> before using
this parameter, otherwise an error will occur. If <code>FALSE</code>
(default), it will return a cloned Series with the flag.
</td>
</tr>
</table>

## Details

Use <code>$flags</code> to see the values of the sorted flags.

## Value

A Series with a flag

## Examples

``` r
library(polars)

s = as_polars_series(1:4)$set_sorted()
s$flags
```

    #> $SORTED_ASC
    #> [1] TRUE
    #> 
    #> $SORTED_DESC
    #> [1] FALSE
