

# Test if the object a polars DataType

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/is_polars.R#L55)

## Description

Test if the object a polars DataType

## Usage

<pre><code class='language-R'>is_polars_dtype(x, include_unknown = FALSE)
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
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="include_unknown">include_unknown</code>
</td>
<td>
If <code>FALSE</code> (default), <code>pl$Unknown</code> is considered
as an invalid datatype.
</td>
</tr>
</table>

## Value

A logical value

## Examples

``` r
library(polars)

is_polars_dtype(pl$Int64)
```

    #> [1] TRUE

``` r
is_polars_dtype(mtcars)
```

    #> [1] FALSE

``` r
is_polars_dtype(pl$Unknown)
```

    #> [1] FALSE

``` r
is_polars_dtype(pl$Unknown, include_unknown = TRUE)
```

    #> [1] TRUE
