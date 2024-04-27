

# Percentage change

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__expr.R#L2609)

## Description

Computes percentage change (as fraction) between current element and
most- recent non-null element at least <code>n</code> period(s) before
the current element. Computes the change from the previous row by
default.

## Usage

<pre><code class='language-R'>Expr_pct_change(n = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="n">n</code>
</td>
<td>
Periods to shift for computing percent change.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(10L, 11L, 12L, NA_integer_, 12L))$
  with_columns(pct_change = pl$col("a")$pct_change())
```

    #> shape: (5, 2)
    #> ┌──────┬────────────┐
    #> │ a    ┆ pct_change │
    #> │ ---  ┆ ---        │
    #> │ i32  ┆ f64        │
    #> ╞══════╪════════════╡
    #> │ 10   ┆ null       │
    #> │ 11   ┆ 0.1        │
    #> │ 12   ┆ 0.090909   │
    #> │ null ┆ 0.0        │
    #> │ 12   ┆ 0.0        │
    #> └──────┴────────────┘
