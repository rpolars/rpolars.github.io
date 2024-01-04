
# Alias

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/#L)

## Description

Change name of Series

## Usage

<pre><code class='language-R'>Series_alias(name)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_alias_:_name">name</code>
</td>
<td>
a String as the new name
</td>
</tr>
</table>

## Value

Series

## Examples

``` r
library(polars)

pl$Series(1:3, name = "alice")$alias("bob")
```

    #> polars Series: shape: (3,)
    #> Series: 'bob' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #> ]
