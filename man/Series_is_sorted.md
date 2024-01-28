

# is_sorted

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/series__series.R#L716)

## Description

is_sorted

## Usage

<pre><code class='language-R'>Series_is_sorted(descending = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_is_sorted_:_descending">descending</code>
</td>
<td>
Check if the Series is sorted in descending order.
</td>
</tr>
</table>

## Details

property sorted flags are not settable, use set_sorted

## Value

DataType

## Examples

``` r
library(polars)

pl$Series(1:4)$sort()$is_sorted()
```

    #> [1] TRUE
