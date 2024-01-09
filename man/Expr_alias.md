
# Rename Expr output

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/#L)

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
