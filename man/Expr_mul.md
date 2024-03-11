

# Multiply two expressions

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/expr__expr.R#L329)

## Description

Method equivalent of multiplication operator <code>expr \* other</code>.

## Usage

<pre><code class='language-R'>Expr_mul(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_mul_:_other">other</code>
</td>
<td>
Numeric literal or expression value.
</td>
</tr>
</table>

## Value

Expr

## See Also

<ul>
<li>

Arithmetic operators

</li>
</ul>

## Examples

``` r
library(polars)

df = pl$DataFrame(x = c(1, 2, 4, 8, 16))

df$with_columns(
  `x*2` = pl$col("x")$mul(2),
  `x * xlog2` = pl$col("x")$mul(pl$col("x")$log(2))
)
```

    #> shape: (5, 3)
    #> ┌──────┬──────┬───────────┐
    #> │ x    ┆ x*2  ┆ x * xlog2 │
    #> │ ---  ┆ ---  ┆ ---       │
    #> │ f64  ┆ f64  ┆ f64       │
    #> ╞══════╪══════╪═══════════╡
    #> │ 1.0  ┆ 2.0  ┆ 0.0       │
    #> │ 2.0  ┆ 4.0  ┆ 2.0       │
    #> │ 4.0  ┆ 8.0  ┆ 8.0       │
    #> │ 8.0  ┆ 16.0 ┆ 24.0      │
    #> │ 16.0 ┆ 32.0 ┆ 64.0      │
    #> └──────┴──────┴───────────┘
