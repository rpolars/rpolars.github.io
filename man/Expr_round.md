
# Round

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/expr__expr.R#L1374)

## Description

Round underlying floating point data by <code>decimals</code> digits.

## Usage

<pre><code class='language-R'>Expr_round(decimals)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_round_:_decimals">decimals</code>
</td>
<td>
Number of decimals to round by.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(0.33, 0.5, 1.02, 1.5, NaN, NA, Inf, -Inf))$with_columns(
  round = pl$col("a")$round(1)
)
```

    #> shape: (8, 2)
    #> ┌──────┬───────┐
    #> │ a    ┆ round │
    #> │ ---  ┆ ---   │
    #> │ f64  ┆ f64   │
    #> ╞══════╪═══════╡
    #> │ 0.33 ┆ 0.3   │
    #> │ 0.5  ┆ 0.5   │
    #> │ 1.02 ┆ 1.0   │
    #> │ 1.5  ┆ 1.5   │
    #> │ NaN  ┆ NaN   │
    #> │ null ┆ null  │
    #> │ inf  ┆ inf   │
    #> │ -inf ┆ -inf  │
    #> └──────┴───────┘
