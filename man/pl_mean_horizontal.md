

# Compute the mean rowwise

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/functions__lazy.R#L965)

## Description

Compute the mean rowwise

## Usage

<pre><code class='language-R'>pl_mean_horizontal(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_mean_horizontal_:_...">…</code>
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
  a = c(1, 8, 3, 6, 7),
  b = c(4, 5, NA_real_, Inf, NaN)
)

df$with_columns(
  pl$mean_horizontal("a", "b")$alias("mean"),
  pl$mean_horizontal("a", "b", 5)$alias("mean_with_lit")
)
```

    #> shape: (5, 4)
    #> ┌─────┬──────┬──────┬───────────────┐
    #> │ a   ┆ b    ┆ mean ┆ mean_with_lit │
    #> │ --- ┆ ---  ┆ ---  ┆ ---           │
    #> │ f64 ┆ f64  ┆ f64  ┆ f64           │
    #> ╞═════╪══════╪══════╪═══════════════╡
    #> │ 1.0 ┆ 4.0  ┆ 2.5  ┆ 3.333333      │
    #> │ 8.0 ┆ 5.0  ┆ 6.5  ┆ 6.0           │
    #> │ 3.0 ┆ null ┆ 3.0  ┆ 4.0           │
    #> │ 6.0 ┆ inf  ┆ inf  ┆ inf           │
    #> │ 7.0 ┆ NaN  ┆ NaN  ┆ NaN           │
    #> └─────┴──────┴──────┴───────────────┘
