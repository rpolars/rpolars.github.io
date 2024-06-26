

# Exponentiation two expressions

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L350)

## Description

Method equivalent of exponentiation operator <code>expr ^
exponent</code>.

## Usage

<pre><code class='language-R'>Expr_pow(exponent)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="exponent">exponent</code>
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

df = pl$DataFrame(x = c(1, 2, 4, 8))

df$with_columns(
  cube = pl$col("x")$pow(3),
  `x^xlog2` = pl$col("x")$pow(pl$col("x")$log(2))
)
```

    #> shape: (4, 3)
    #> ┌─────┬───────┬─────────┐
    #> │ x   ┆ cube  ┆ x^xlog2 │
    #> │ --- ┆ ---   ┆ ---     │
    #> │ f64 ┆ f64   ┆ f64     │
    #> ╞═════╪═══════╪═════════╡
    #> │ 1.0 ┆ 1.0   ┆ 1.0     │
    #> │ 2.0 ┆ 8.0   ┆ 2.0     │
    #> │ 4.0 ┆ 64.0  ┆ 16.0    │
    #> │ 8.0 ┆ 512.0 ┆ 512.0   │
    #> └─────┴───────┴─────────┘
