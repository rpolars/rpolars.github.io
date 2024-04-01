

# Return the element at the given index

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L1070)

## Description

Return the element at the given index

## Usage

<pre><code class='language-R'>Series_item(index = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_item_:_index">index</code>
</td>
<td>
Index of the item to return.
</td>
</tr>
</table>

## Value

A value of length 1

## Examples

``` r
library(polars)

s1 = pl$Series(values = 1)

s1$item()
```

    #> [1] 1

``` r
s2 = pl$Series(values = 9:7)

s2$cum_sum()$item(-1)
```

    #> [1] 24
