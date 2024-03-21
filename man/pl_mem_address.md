

# Get Memory Address

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/after-wrappers.R#L319)

## Description

Get underlying mem address a rust object (via ExtPtr). Expert use only.

## Usage

<pre><code class='language-R'>pl_mem_address(robj)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_mem_address_:_robj">robj</code>
</td>
<td>
an R object
</td>
</tr>
</table>

## Details

Does not give meaningful answers for regular R objects.

## Value

String of mem address

## Examples

``` r
library(polars)

pl$mem_address(pl$Series(1:3))
```

    #> [1] "0x7fd5f3071030"
