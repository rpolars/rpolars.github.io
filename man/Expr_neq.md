

# Check inequality

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/expr__expr.R#L467)

## Description

Method equivalent of addition operator <code>expr + other</code>.

## Usage

<pre><code class='language-R'>Expr_neq(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_neq_:_other">other</code>
</td>
<td>
numeric or string value; accepts expression input.
</td>
</tr>
</table>

## Value

Expr

## See Also

Expr_neq_missing

## Examples

``` r
library(polars)

pl$lit(1) != 2
```

    #> polars Expr: [(1.0) != (2.0)]

``` r
pl$lit(1) != pl$lit(2)
```

    #> polars Expr: [(1.0) != (2.0)]

``` r
pl$lit(1)$neq(pl$lit(2))
```

    #> polars Expr: [(1.0) != (2.0)]
