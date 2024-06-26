

# Test if the object is a polars LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/is_polars.R#L25)

## Description

This function tests if the object is a polars LazyFrame.

## Usage

<pre><code class='language-R'>is_polars_lf(x)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="x">x</code>
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

is_polars_lf(mtcars)
```

    #> [1] FALSE

``` r
is_polars_lf(as_polars_lf(mtcars))
```

    #> [1] TRUE
