

# Compute the mean rowwise

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L966)

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
  a = c(1, 8, 3),
  b = c(4, 5, NA_real_),
  c = c("x", "y", "z")
)
df$with_columns(
  pl$mean_horizontal("a", "b")$alias("mean")
)
```

    #> shape: (3, 4)
    #> ┌─────┬──────┬─────┬──────┐
    #> │ a   ┆ b    ┆ c   ┆ mean │
    #> │ --- ┆ ---  ┆ --- ┆ ---  │
    #> │ f64 ┆ f64  ┆ str ┆ f64  │
    #> ╞═════╪══════╪═════╪══════╡
    #> │ 1.0 ┆ 4.0  ┆ x   ┆ 2.5  │
    #> │ 8.0 ┆ 5.0  ┆ y   ┆ 6.5  │
    #> │ 3.0 ┆ null ┆ z   ┆ 3.0  │
    #> └─────┴──────┴─────┴──────┘
