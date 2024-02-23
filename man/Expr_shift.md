

# Shift values

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/expr__expr.R#L1635)

## Description

Shift values

## Usage

<pre><code class='language-R'>Expr_shift(periods = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_shift_:_periods">periods</code>
</td>
<td>
Number of periods to shift, may be negative.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(1, 2, 4, 5, 8))$
  with_columns(
  pl$col("a")$shift(-2)$alias("shift-2"),
  pl$col("a")$shift(2)$alias("shift+2")
)
```

    #> shape: (5, 3)
    #> ┌─────┬─────────┬─────────┐
    #> │ a   ┆ shift-2 ┆ shift+2 │
    #> │ --- ┆ ---     ┆ ---     │
    #> │ f64 ┆ f64     ┆ f64     │
    #> ╞═════╪═════════╪═════════╡
    #> │ 1.0 ┆ 4.0     ┆ null    │
    #> │ 2.0 ┆ 5.0     ┆ null    │
    #> │ 4.0 ┆ 8.0     ┆ 1.0     │
    #> │ 5.0 ┆ null    ┆ 2.0     │
    #> │ 8.0 ┆ null    ┆ 4.0     │
    #> └─────┴─────────┴─────────┘
