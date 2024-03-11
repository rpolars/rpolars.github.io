

# Check greater or equal inequality

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/expr__expr.R#L526)

## Description

Method equivalent of addition operator <code>expr + other</code>.

## Usage

<pre><code class='language-R'>Expr_gt_eq(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_gt_eq_:_other">other</code>
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

pl$lit(2) >= 2
```

    #> polars Expr: [(2.0) >= (2.0)]

``` r
pl$lit(2) >= pl$lit(2)
```

    #> polars Expr: [(2.0) >= (2.0)]

``` r
pl$lit(2)$gt_eq(pl$lit(2))
```

    #> polars Expr: [(2.0) >= (2.0)]
