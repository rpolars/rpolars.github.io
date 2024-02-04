

# Index of a sort

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/expr__expr.R#L1445)

## Description

Get the index values that would sort this column.

## Usage

<pre><code class='language-R'>Expr_arg_sort(descending = FALSE, nulls_last = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_arg_sort_:_descending">descending</code>
</td>
<td>
Sort in descending order. When sorting by multiple columns, can be
specified per column by passing a vector of booleans.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_arg_sort_:_nulls_last">nulls_last</code>
</td>
<td>
If <code>TRUE</code>, place nulls values last.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(
  a = c(6, 1, 0, NA, Inf, NaN)
)$with_columns(arg_sorted = pl$col("a")$arg_sort())
```

    #> shape: (6, 2)
    #> ┌──────┬────────────┐
    #> │ a    ┆ arg_sorted │
    #> │ ---  ┆ ---        │
    #> │ f64  ┆ u32        │
    #> ╞══════╪════════════╡
    #> │ 6.0  ┆ 3          │
    #> │ 1.0  ┆ 2          │
    #> │ 0.0  ┆ 1          │
    #> │ null ┆ 0          │
    #> │ inf  ┆ 4          │
    #> │ NaN  ┆ 5          │
    #> └──────┴────────────┘
