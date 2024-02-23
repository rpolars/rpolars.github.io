

# Rename Expr output

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/after-wrappers.R#L20)

## Description

Rename the output of an expression.

## Usage

<pre><code class='language-R'>Expr_alias(name)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_alias_:_name">name</code>
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
