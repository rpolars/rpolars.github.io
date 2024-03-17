

# Get quantile value.

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L1952)

## Description

Get quantile value.

## Usage

<pre><code class='language-R'>Expr_quantile(quantile, interpolation = "nearest")
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_quantile_:_quantile">quantile</code>
</td>
<td>
Either a numeric value or an Expr whose value must be between 0 and 1.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_quantile_:_interpolation">interpolation</code>
</td>
<td>
One of <code>“nearest”</code>, <code>“higher”</code>,
<code>“lower”</code>, <code>“midpoint”</code>, or <code>“linear”</code>.
</td>
</tr>
</table>

## Details

Null values are ignored and <code>NaN</code>s are ranked as the largest
value. For linear interpolation <code>NaN</code> poisons
<code>Inf</code>, that poisons any other value.

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(x = -5:5)$
  select(pl$col("x")$quantile(0.5))
```

    #> shape: (1, 1)
    #> ┌─────┐
    #> │ x   │
    #> │ --- │
    #> │ f64 │
    #> ╞═════╡
    #> │ 0.0 │
    #> └─────┘
