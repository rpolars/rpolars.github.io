

# Substract two expressions

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L311)

## Description

Method equivalent of subtraction operator <code>expr - other</code>.

## Usage

<pre><code class='language-R'>Expr_sub(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_sub_:_other">other</code>
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

df = pl$DataFrame(x = 0:4)

df$with_columns(
  `x-2` = pl$col("x")$sub(2),
  `x-expr` = pl$col("x")$sub(pl$col("x")$cum_sum())
)
```

    #> shape: (5, 3)
    #> ┌─────┬──────┬────────┐
    #> │ x   ┆ x-2  ┆ x-expr │
    #> │ --- ┆ ---  ┆ ---    │
    #> │ i32 ┆ f64  ┆ i32    │
    #> ╞═════╪══════╪════════╡
    #> │ 0   ┆ -2.0 ┆ 0      │
    #> │ 1   ┆ -1.0 ┆ 0      │
    #> │ 2   ┆ 0.0  ┆ -1     │
    #> │ 3   ┆ 1.0  ┆ -3     │
    #> │ 4   ┆ 2.0  ┆ -6     │
    #> └─────┴──────┴────────┘
