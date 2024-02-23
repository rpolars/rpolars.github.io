

# Test if the object is a polars DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/is_polars.R#L11)

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
