
# Rename a series

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/series__series.R#L834)

## Description

Rename a series

## Usage

<pre><code class='language-R'>Series_rename(name, in_place = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_rename_:_name">name</code>
</td>
<td>
string the new name
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_rename_:_in_place">in_place</code>
</td>
<td>
bool rename in-place, breaks immutability If true will throw an error
unless this option has been set: <code>pl$set_options(strictly_immutable
= FALSE)</code>
</td>
</tr>
</table>

## Format

method

## Value

bool

## Examples

``` r
library(polars)

pl$Series(1:4, "bob")$rename("alice")
```

    #> polars Series: shape: (4,)
    #> Series: 'alice' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #>  4
    #> ]
