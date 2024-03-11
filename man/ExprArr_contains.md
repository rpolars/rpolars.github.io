

# Check if array contains a given value

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/expr__array.R#L181)

## Description

Check if array contains a given value

## Usage

<pre><code class='language-R'>ExprArr_contains(item)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprArr_contains_:_item">item</code>
</td>
<td>
Expr or something coercible to an Expr. Strings are <em>not</em> parsed
as columns.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  values = list(0:2, 4:6, c(NA_integer_, NA_integer_, NA_integer_)),
  item = c(0L, 4L, 2L),
  schema = list(values = pl$Array(pl$Float64, 3))
)
df$with_columns(
  with_expr = pl$col("values")$arr$contains(pl$col("item")),
  with_lit = pl$col("values")$arr$contains(1)
)
```

    #> shape: (3, 4)
    #> ┌────────────────────┬──────┬───────────┬──────────┐
    #> │ values             ┆ item ┆ with_expr ┆ with_lit │
    #> │ ---                ┆ ---  ┆ ---       ┆ ---      │
    #> │ array[f64, 3]      ┆ i32  ┆ bool      ┆ bool     │
    #> ╞════════════════════╪══════╪═══════════╪══════════╡
    #> │ [0.0, 1.0, 2.0]    ┆ 0    ┆ true      ┆ true     │
    #> │ [4.0, 5.0, 6.0]    ┆ 4    ┆ true      ┆ false    │
    #> │ [null, null, null] ┆ 2    ┆ false     ┆ false    │
    #> └────────────────────┴──────┴───────────┴──────────┘
