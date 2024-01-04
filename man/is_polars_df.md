
# Test if the object is a polars DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/is_polars.R#L11)

## Description

These functions test if the object is a polars DataFrame.

## Usage

<pre><code class='language-R'>is_polars_df(x)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="is_polars_df_:_x">x</code>
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

is_polars_df(mtcars)
```

    #> [1] FALSE

``` r
is_polars_df(as_polars_df(mtcars))
```

    #> [1] TRUE
