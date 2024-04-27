

# Check inequality

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__expr.R#L467)

## Description

Method equivalent of addition operator <code>expr + other</code>.

## Usage

<pre><code class='language-R'>Expr_neq(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="other">other</code>
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
