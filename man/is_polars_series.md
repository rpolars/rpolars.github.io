

# Test if the object is a polars Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/is_polars.R#L39)

## Description

This function tests if the object is a polars Series.

## Usage

<pre><code class='language-R'>is_polars_series(x)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="is_polars_series_:_x">x</code>
</td>
<td>
An object
</td>
</tr>
</table>

## Value

A logical value

## Examples

``` r
library(polars)

is_polars_series(1:3)
```

    #> [1] FALSE

``` r
is_polars_series(as_polars_series(1:3))
```

    #> [1] TRUE
