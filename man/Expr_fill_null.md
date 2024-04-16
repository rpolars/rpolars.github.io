

# Fill null values with a value or strategy

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/expr__expr.R#L1592)

## Description

Fill null values with a value or strategy

## Usage

<pre><code class='language-R'>Expr_fill_null(value = NULL, strategy = NULL, limit = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_fill_null_:_value">value</code>
</td>
<td>
Expr or something coercible in an Expr
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_fill_null_:_strategy">strategy</code>
</td>
<td>
Possible choice are <code>NULL</code> (default, requires a non-null
<code>value</code>), <code>“forward”</code>, <code>“backward”</code>,
<code>“min”</code>, <code>“max”</code>, <code>“mean”</code>,
<code>“zero”</code>, <code>“one”</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_fill_null_:_limit">limit</code>
</td>
<td>
Number of consecutive null values to fill when using the
<code>“forward”</code> or <code>“backward”</code> strategy.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(NA, 1, NA, 2, NA))$
  with_columns(
  value = pl$col("a")$fill_null(999),
  backward = pl$col("a")$fill_null(strategy = "backward"),
  mean = pl$col("a")$fill_null(strategy = "mean")
)
```

    #> shape: (5, 4)
    #> ┌──────┬───────┬──────────┬──────┐
    #> │ a    ┆ value ┆ backward ┆ mean │
    #> │ ---  ┆ ---   ┆ ---      ┆ ---  │
    #> │ f64  ┆ f64   ┆ f64      ┆ f64  │
    #> ╞══════╪═══════╪══════════╪══════╡
    #> │ null ┆ 999.0 ┆ 1.0      ┆ 1.5  │
    #> │ 1.0  ┆ 1.0   ┆ 1.0      ┆ 1.0  │
    #> │ null ┆ 999.0 ┆ 2.0      ┆ 1.5  │
    #> │ 2.0  ┆ 2.0   ┆ 2.0      ┆ 2.0  │
    #> │ null ┆ 999.0 ┆ null     ┆ 1.5  │
    #> └──────┴───────┴──────────┴──────┘
