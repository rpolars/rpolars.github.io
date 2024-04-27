

# Modulo two expressions

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__expr.R#L294)

## Description

Method equivalent of modulus operator <code>expr %% other</code>.

## Usage

<pre><code class='language-R'>Expr_mod(other)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="other">other</code>
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

<code>\<Expr\>$floor_div()</code>

</li>
</ul>

## Examples

``` r
library(polars)

df = pl$DataFrame(x = -5L:5L)

df$with_columns(
  `x%%2` = pl$col("x")$mod(2)
)
```

    #> shape: (11, 2)
    #> ┌─────┬──────┐
    #> │ x   ┆ x%%2 │
    #> │ --- ┆ ---  │
    #> │ i32 ┆ f64  │
    #> ╞═════╪══════╡
    #> │ -5  ┆ 1.0  │
    #> │ -4  ┆ 0.0  │
    #> │ -3  ┆ 1.0  │
    #> │ -2  ┆ 0.0  │
    #> │ -1  ┆ 1.0  │
    #> │ …   ┆ …    │
    #> │ 1   ┆ 1.0  │
    #> │ 2   ┆ 0.0  │
    #> │ 3   ┆ 1.0  │
    #> │ 4   ┆ 0.0  │
    #> │ 5   ┆ 1.0  │
    #> └─────┴──────┘
