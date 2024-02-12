

# Variance

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L611)

## Description

syntactic sugar for starting a expression with var

## Usage

<pre><code class='language-R'>pl_var(column, ddof = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_var_:_column">column</code>
</td>
<td>
Column name.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_var_:_ddof">ddof</code>
</td>
<td>
Delta Degrees of Freedom: the divisor used in the calculation is N -
ddof, where N represents the number of elements. By default ddof is 1.
</td>
</tr>
</table>

## Value

Expr or Series matching type of input column
