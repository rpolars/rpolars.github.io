

# Get the value by index in an array

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/expr__array.R#L115)

## Description

This allows to extract one value per array only.

## Usage

<pre><code class='language-R'>ExprArr_get(index)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprArr_get_:_index">index</code>
</td>
<td>
An Expr or something coercible to an Expr, that must return a single
index. Values are 0-indexed (so index 0 would return the first item of
every sub-array) and negative values start from the end (index
<code>-1</code> returns the last item). If the index is out of bounds,
it will return a <code>null</code>. Strings are parsed as column names.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  values = list(c(1, 2), c(3, 4), c(NA_real_, 6)),
  idx = c(1, NA, 3),
  schema = list(values = pl$Array(pl$Float64, 2))
)
df$with_columns(
  using_expr = pl$col("values")$arr$get("idx"),
  val_0 = pl$col("values")$arr$get(0),
  val_minus_1 = pl$col("values")$arr$get(-1),
  val_oob = pl$col("values")$arr$get(10)
)
```

    #> shape: (3, 6)
    #> ┌───────────────┬──────┬────────────┬───────┬─────────────┬─────────┐
    #> │ values        ┆ idx  ┆ using_expr ┆ val_0 ┆ val_minus_1 ┆ val_oob │
    #> │ ---           ┆ ---  ┆ ---        ┆ ---   ┆ ---         ┆ ---     │
    #> │ array[f64, 2] ┆ f64  ┆ f64        ┆ f64   ┆ f64         ┆ f64     │
    #> ╞═══════════════╪══════╪════════════╪═══════╪═════════════╪═════════╡
    #> │ [1.0, 2.0]    ┆ 1.0  ┆ 2.0        ┆ 1.0   ┆ 2.0         ┆ null    │
    #> │ [3.0, 4.0]    ┆ null ┆ null       ┆ 3.0   ┆ 4.0         ┆ null    │
    #> │ [null, 6.0]   ┆ 3.0  ┆ null       ┆ null  ┆ 6.0         ┆ null    │
    #> └───────────────┴──────┴────────────┴───────┴─────────────┴─────────┘
