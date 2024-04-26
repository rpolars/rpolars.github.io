

# Check strictly lower inequality

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L384)

## Description

Method equivalent of addition operator <code>expr + other</code>.

## Usage

<pre><code class='language-R'>Expr_lt(other)
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

## Examples

``` r
library(polars)

pl$lit(5) < 10
```

    #> polars Expr: [(5.0) < (10.0)]

``` r
pl$lit(5) < pl$lit(10)
```

    #> polars Expr: [(5.0) < (10.0)]

``` r
pl$lit(5)$lt(pl$lit(10))
```

    #> polars Expr: [(5.0) < (10.0)]
