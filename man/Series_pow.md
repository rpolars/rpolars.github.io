

# Power Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/series__series.R#L475)

## Description

Method equivalent of power operator <code>series ^ other</code>.

## Usage

<pre><code class='language-R'>Series_pow(exponent)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_pow_:_exponent">exponent</code>
</td>
<td>
Series like object of numeric. Converted to Series by
<code>as_polars_series()</code> in this method.
</td>
</tr>
</table>

## Value

Series

## See Also

<ul>
<li>

Arithmetic operators

</li>
</ul>

## Examples

``` r
library(polars)

s = as_polars_series(1:4, name = "foo")

s$pow(3L)
```

    #> polars Series: shape: (4,)
    #> Series: 'foo' [i32]
    #> [
    #>  1
    #>  8
    #>  27
    #>  64
    #> ]
