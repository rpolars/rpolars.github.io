

# Rename a series

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/series__series.R#L828)

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
unless this option has been set: <code>options(polars.strictly_immutable
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
