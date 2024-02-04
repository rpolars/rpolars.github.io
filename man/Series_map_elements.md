

# Apply every value with an R fun

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/series__series.R#L362)

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
<code id="Series_map_elements_:_fun">fun</code>
</td>
<td>
r function, should take a scalar value as input and return one.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_map_elements_:_datatype">datatype</code>
</td>
<td>
DataType of return value. Default NULL means same as input.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_map_elements_:_strict_return_type">strict_return_type</code>
</td>
<td>
bool, default TRUE: fail on wrong return type, FALSE: convert to polars
Null
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_map_elements_:_allow_fail_eval">allow_fail_eval</code>
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

s = pl$Series(letters[1:5], "ltrs")
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
pl$Series(sapply(s$to_r(), f), s$name)
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
