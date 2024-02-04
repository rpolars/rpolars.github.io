

# Set sorted

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/series__series.R#L747)

## Description

Set sorted

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
if TRUE, will set flag mutably and return NULL. Remember to use
options(polars.strictly_immutable = FALSE) otherwise an error will be
thrown. If FALSE will return a cloned Series with set_flag which in the
very most cases should be just fine.
</td>
</tr>
</table>

## Value

Series invisible

## Examples

``` r
library(polars)

s = pl$Series(1:4)$set_sorted()
s$flags
```

    #> $SORTED_ASC
    #> [1] TRUE
    #> 
    #> $SORTED_DESC
    #> [1] FALSE
