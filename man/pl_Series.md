

# Create new Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/series__series.R#L66)

## Description

found in api as pl$Series named Series_constructor internally

## Usage

<pre><code class='language-R'>pl_Series(x, name = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_Series_:_x">x</code>
</td>
<td>
any vector
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_Series_:_name">name</code>
</td>
<td>
string
</td>
</tr>
</table>

## Value

Series

## Examples

``` r
library(polars)

{
  pl$Series(1:4)
}
```

    #> polars Series: shape: (4,)
    #> Series: '' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #>  4
    #> ]
