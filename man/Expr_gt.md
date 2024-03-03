

# Check strictly greater inequality

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L404)

## Description

Method equivalent of addition operator <code>expr + other</code>.

## Usage

<pre><code class='language-R'>Expr_gt(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_gt_:_other">other</code>
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

pl$lit(2) > 1
```

    #> polars Expr: [(2.0) > (1.0)]

``` r
pl$lit(2) > pl$lit(1)
```

    #> polars Expr: [(2.0) > (1.0)]

``` r
pl$lit(2)$gt(pl$lit(1))
```

    #> polars Expr: [(2.0) > (1.0)]
