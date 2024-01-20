
# Exponentiation

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L2086)

## Description

Raise expression to the power of exponent.

## Usage

<pre><code class='language-R'>Expr_pow(exponent)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_pow_:_exponent">exponent</code>
</td>
<td>
Exponent value.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

# use via `pow`-method and the `^`-operator
pl$DataFrame(a = -1:3, b = 2:6)$with_columns(
  x = pl$col("a")$pow(2),
  y = pl$col("a")^3
)
```

    #> shape: (5, 4)
    #> ┌─────┬─────┬─────┬──────┐
    #> │ a   ┆ b   ┆ x   ┆ y    │
    #> │ --- ┆ --- ┆ --- ┆ ---  │
    #> │ i32 ┆ i32 ┆ f64 ┆ f64  │
    #> ╞═════╪═════╪═════╪══════╡
    #> │ -1  ┆ 2   ┆ 1.0 ┆ -1.0 │
    #> │ 0   ┆ 3   ┆ 0.0 ┆ 0.0  │
    #> │ 1   ┆ 4   ┆ 1.0 ┆ 1.0  │
    #> │ 2   ┆ 5   ┆ 4.0 ┆ 8.0  │
    #> │ 3   ┆ 6   ┆ 9.0 ┆ 27.0 │
    #> └─────┴─────┴─────┴──────┘
