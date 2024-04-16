

# Floor divide two expressions

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/expr__expr.R#L276)

## Description

Method equivalent of floor division operator <code>expr %/%
other</code>.

## Usage

<pre><code class='language-R'>Expr_floor_div(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_floor_div_:_other">other</code>
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
<li>

<code>\<Expr\>$div()</code>

</li>
<li>

<code>\<Expr\>$mod()</code>

</li>
</ul>

## Examples

``` r
library(polars)

df = pl$DataFrame(x = 1:5)

df$with_columns(
  `x/2` = pl$col("x")$div(2),
  `x%/%2` = pl$col("x")$floor_div(2)
)
```

    #> shape: (5, 3)
    #> ┌─────┬─────┬───────┐
    #> │ x   ┆ x/2 ┆ x%/%2 │
    #> │ --- ┆ --- ┆ ---   │
    #> │ i32 ┆ f64 ┆ f64   │
    #> ╞═════╪═════╪═══════╡
    #> │ 1   ┆ 0.5 ┆ 0.0   │
    #> │ 2   ┆ 1.0 ┆ 1.0   │
    #> │ 3   ┆ 1.5 ┆ 1.0   │
    #> │ 4   ┆ 2.0 ┆ 2.0   │
    #> │ 5   ┆ 2.5 ┆ 2.0   │
    #> └─────┴─────┴───────┘
