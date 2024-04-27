

# Rename Expr output

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/after-wrappers.R#L20)

## Description

Rename the output of an expression.

## Usage

<pre><code class='language-R'>Expr_alias(name)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="name">name</code>
</td>
<td>
New name of output
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$col("bob")$alias("alice")
```

    #> polars Expr: col("bob").alias("alice")
