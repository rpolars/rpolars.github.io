
# Compute the sum rowwise

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L1006)

## Description

Compute the sum rowwise

## Usage

<pre><code class='language-R'>pl_sum_horizontal(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_sum_horizontal_:_...">…</code>
</td>
<td>
Columns to concatenate into a single string column. Accepts expressions.
Strings are parsed as column names, other non-expression inputs are
parsed as literals.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = NA_real_,
  b = c(3:4, NA_real_, NA_real_),
  c = c(1:2, NA_real_, -Inf)
)
df$with_columns(
  pl$sum_horizontal("a", "b", "c", 2)$alias("sum")
)
```

    #> shape: (4, 4)
    #> ┌──────┬──────┬──────┬──────┐
    #> │ a    ┆ b    ┆ c    ┆ sum  │
    #> │ ---  ┆ ---  ┆ ---  ┆ ---  │
    #> │ f64  ┆ f64  ┆ f64  ┆ f64  │
    #> ╞══════╪══════╪══════╪══════╡
    #> │ null ┆ 3.0  ┆ 1.0  ┆ 6.0  │
    #> │ null ┆ 4.0  ┆ 2.0  ┆ 8.0  │
    #> │ null ┆ null ┆ null ┆ 2.0  │
    #> │ null ┆ null ┆ -inf ┆ -inf │
    #> └──────┴──────┴──────┴──────┘
