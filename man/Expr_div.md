

# Divide two expressions

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L255)

## Description

Method equivalent of float division operator <code>expr / other</code>.

## Usage

<pre><code class='language-R'>Expr_div(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_div_:_other">other</code>
</td>
<td>
Numeric literal or expression value.
</td>
</tr>
</table>

## Details

Zero-division behaviour follows IEEE-754:

<ul>
<li>

<code>0/0</code>: Invalid operation - mathematically undefined, returns
<code>NaN</code>.

</li>
<li>

<code>n/0</code>: On finite operands gives an exact infinite result, eg:
±infinity.

</li>
</ul>

## Value

Expr

## See Also

<ul>
<li>

Arithmetic operators

</li>
<li>

<code>\<Expr\>$floor_div()</code>

</li>
</ul>

## Examples

``` r
library(polars)

df = pl$DataFrame(
  x = -2:2,
  y = c(0.5, 0, 0, -4, -0.5)
)

df$with_columns(
  `x/2` = pl$col("x")$div(2),
  `x/y` = pl$col("x")$div(pl$col("y"))
)
```

    #> shape: (5, 4)
    #> ┌─────┬──────┬──────┬───────┐
    #> │ x   ┆ y    ┆ x/2  ┆ x/y   │
    #> │ --- ┆ ---  ┆ ---  ┆ ---   │
    #> │ i32 ┆ f64  ┆ f64  ┆ f64   │
    #> ╞═════╪══════╪══════╪═══════╡
    #> │ -2  ┆ 0.5  ┆ -1.0 ┆ -4.0  │
    #> │ -1  ┆ 0.0  ┆ -0.5 ┆ -inf  │
    #> │ 0   ┆ 0.0  ┆ 0.0  ┆ NaN   │
    #> │ 1   ┆ -4.0 ┆ 0.5  ┆ -0.25 │
    #> │ 2   ┆ -0.5 ┆ 1.0  ┆ -4.0  │
    #> └─────┴──────┴──────┴───────┘
