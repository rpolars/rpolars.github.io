

# Get the minimum value rowwise

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L836)

## Description

Get the minimum value rowwise

## Usage

<pre><code class='language-R'>pl_min_horizontal(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_min_horizontal_:_...">…</code>
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
  b = c(2:1, NA_real_, NA_real_),
  c = c(1:2, NA_real_, -Inf)
)
df$with_columns(
  pl$min_horizontal("a", "b", "c", 99.9)$alias("min")
)
```

    #> shape: (4, 4)
    #> ┌──────┬──────┬──────┬──────┐
    #> │ a    ┆ b    ┆ c    ┆ min  │
    #> │ ---  ┆ ---  ┆ ---  ┆ ---  │
    #> │ f64  ┆ f64  ┆ f64  ┆ f64  │
    #> ╞══════╪══════╪══════╪══════╡
    #> │ null ┆ 2.0  ┆ 1.0  ┆ 1.0  │
    #> │ null ┆ 1.0  ┆ 2.0  ┆ 1.0  │
    #> │ null ┆ null ┆ null ┆ 99.9 │
    #> │ null ┆ null ┆ -inf ┆ -inf │
    #> └──────┴──────┴──────┴──────┘
