

# Fill NaN

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L1655)

## Description

Fill NaN

## Usage

<pre><code class='language-R'>Expr_fill_nan(expr = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="expr">expr</code>
</td>
<td>
Expr or something coercible in an Expr
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(NaN, 1, NaN, 2, NA))$
  with_columns(
  literal = pl$col("a")$fill_nan(999),
  # implicit coercion to string
  string = pl$col("a")$fill_nan("invalid")
)
```

    #> shape: (5, 3)
    #> ┌──────┬─────────┬─────────┐
    #> │ a    ┆ literal ┆ string  │
    #> │ ---  ┆ ---     ┆ ---     │
    #> │ f64  ┆ f64     ┆ str     │
    #> ╞══════╪═════════╪═════════╡
    #> │ NaN  ┆ 999.0   ┆ invalid │
    #> │ 1.0  ┆ 1.0     ┆ 1.0     │
    #> │ NaN  ┆ 999.0   ┆ invalid │
    #> │ 2.0  ┆ 2.0     ┆ 2.0     │
    #> │ null ┆ null    ┆ null    │
    #> └──────┴─────────┴─────────┘
