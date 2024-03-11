

# Var

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/series__series.R#L837)

## Description

Aggregate the columns of this Series to their variance values.

## Usage

<pre><code class='language-R'>Series_var(ddof = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_var_:_ddof">ddof</code>
</td>
<td>
integer Delta Degrees of Freedom: the divisor used in the calculation is
N - ddof, where N represents the number of elements. By default ddof is
1.
</td>
</tr>
</table>

## Value

A new <code>Series</code> object with applied aggregation.

## Examples

``` r
library(polars)

pl$Series(1:10)$var()
```

    #> [1] 9.166667
