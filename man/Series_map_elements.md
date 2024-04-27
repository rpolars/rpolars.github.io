

# Apply every value with an R fun

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/series__series.R#L609)

## Description

About as slow as regular non-vectorized R. Similar to using R sapply on
a vector.

## Usage

<pre><code class='language-R'>Series_map_elements(
  fun,
  datatype = NULL,
  strict_return_type = TRUE,
  allow_fail_eval = FALSE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="fun">fun</code>
</td>
<td>
r function, should take a single value as input and return one.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="datatype">datatype</code>
</td>
<td>
DataType of return value. Default NULL means same as input.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="strict_return_type">strict_return_type</code>
</td>
<td>
bool, default TRUE: fail on wrong return type, FALSE: convert to polars
Null
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="allow_fail_eval">allow_fail_eval</code>
</td>
<td>
bool, default FALSE: raise R fun error, TRUE: convert to polars Null
</td>
</tr>
</table>

## Value

Series

## Examples

``` r
library(polars)

s = as_polars_series(letters[1:5], "ltrs")
f = \(x) paste(x, ":", as.integer(charToRaw(x)))
s$map_elements(f, pl$String)
```

    #> polars Series: shape: (5,)
    #> Series: 'ltrs_apply' [str]
    #> [
    #>  "a : 97"
    #>  "b : 98"
    #>  "c : 99"
    #>  "d : 100"
    #>  "e : 101"
    #> ]

``` r
# same as
as_polars_series(sapply(s$to_r(), f), s$name)
```

    #> polars Series: shape: (5,)
    #> Series: 'ltrs' [str]
    #> [
    #>  "a : 97"
    #>  "b : 98"
    #>  "c : 99"
    #>  "d : 100"
    #>  "e : 101"
    #> ]
