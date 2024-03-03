

# Power Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/series__series.R#L376)

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
    #> Series: 'foo' [f64]
    #> [
    #>  1.0
    #>  8.0
    #>  27.0
    #>  64.0
    #> ]
