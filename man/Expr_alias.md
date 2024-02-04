

# Rename Expr output

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/after-wrappers.R#L20)

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
