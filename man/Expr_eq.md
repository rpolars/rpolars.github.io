

# Check equality

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/expr__expr.R#L428)

## Description

Method equivalent of addition operator <code>expr + other</code>.

## Usage

<pre><code class='language-R'>Expr_eq(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_eq_:_other">other</code>
</td>
<td>
numeric or string value; accepts expression input.
</td>
</tr>
</table>

## Value

Expr

## See Also

Expr_eq_missing

## Examples

``` r
library(polars)

pl$lit(2) == 2
```

    #> polars Expr: [(2.0) == (2.0)]

``` r
pl$lit(2) == pl$lit(2)
```

    #> polars Expr: [(2.0) == (2.0)]

``` r
pl$lit(2)$eq(pl$lit(2))
```

    #> polars Expr: [(2.0) == (2.0)]
