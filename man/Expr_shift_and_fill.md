

# Shift and fill values

[**Source code**](https://github.com/pola-rs/r-polars/tree/mkdocs-matrial-search-preview/R/expr__expr.R#L1626)

## Description

Shift the values by a given period and fill the resulting null values.

## Usage

<pre><code class='language-R'>Expr_shift_and_fill(periods, fill_value)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_shift_and_fill_:_periods">periods</code>
</td>
<td>
Number of periods to shift, may be negative.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_shift_and_fill_:_fill_value">fill_value</code>
</td>
<td>
Fill null values with the result of this expression.
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
  pl$col("a")$shift_and_fill(-2, fill_value = 42)$alias("shift-2"),
  pl$col("a")$shift_and_fill(2, fill_value = pl$col("a") / 2)$alias("shift+2")
)
```

    #> shape: (5, 3)
    #> ┌─────┬─────────┬─────────┐
    #> │ a   ┆ shift-2 ┆ shift+2 │
    #> │ --- ┆ ---     ┆ ---     │
    #> │ f64 ┆ f64     ┆ f64     │
    #> ╞═════╪═════════╪═════════╡
    #> │ 1.0 ┆ 4.0     ┆ 0.5     │
    #> │ 2.0 ┆ 5.0     ┆ 0.5     │
    #> │ 4.0 ┆ 8.0     ┆ 1.0     │
    #> │ 5.0 ┆ 42.0    ┆ 2.0     │
    #> │ 8.0 ┆ 42.0    ┆ 4.0     │
    #> └─────┴─────────┴─────────┘
