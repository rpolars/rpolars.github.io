

# Test if the object is a polars DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/is_polars.R#L11)

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
