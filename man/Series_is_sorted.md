

# Check if the Series is sorted

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L809)

## Description

Check if the Series is sorted

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

## Value

A logical value

## See Also

Use <code>$set_sorted()</code> to add a "sorted" flag to the Series that
could be used for faster operations later on.

## Examples

``` r
library(polars)

as_polars_series(1:4)$sort()$is_sorted()
```

    #> [1] TRUE
