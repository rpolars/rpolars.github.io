

# Set a sorted flag on a Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L844)

## Description

Set a sorted flag on a Series

## Usage

<pre><code class='language-R'>Series_set_sorted(descending = FALSE, in_place = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_set_sorted_:_descending">descending</code>
</td>
<td>
Sort the columns in descending order.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_set_sorted_:_in_place">in_place</code>
</td>
<td>
If <code>TRUE</code>, this will set the flag mutably and return NULL.
Remember to use <code>options(polars.strictly_immutable = FALSE)</code>
before using this parameter, otherwise an error will occur. If
<code>FALSE</code> (default), it will return a cloned Series with the
flag.
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
