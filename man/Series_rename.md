

# Rename a series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L935)

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
New name.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_rename_:_in_place">in_place</code>
</td>
<td>
Rename in-place, which breaks immutability. If <code>TRUE</code>, you
need to run <code>options(polars.strictly_immutable = FALSE)</code>
before, otherwise it will throw an error.
</td>
</tr>
</table>

## Value

Series

## Examples

``` r
library(polars)

as_polars_series(1:4, "bob")$rename("alice")
```

    #> polars Series: shape: (4,)
    #> Series: 'alice' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #>  4
    #> ]
