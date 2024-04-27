

# Get unique values in an array

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__array.R#L128)

## Description

Get unique values in an array

## Usage

<pre><code class='language-R'>ExprArr_unique(maintain_order = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="maintain_order">maintain_order</code>
</td>
<td>
If <code>TRUE</code>, the unique values are returned in order of
appearance.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  values = list(c(1, 1, 2), c(4, 4, 4), c(NA_real_, 6, 7)),
  schema = list(values = pl$Array(pl$Float64, 3))
)
df$with_columns(unique = pl$col("values")$arr$unique())
```

    #> shape: (3, 2)
    #> ┌──────────────────┬──────────────────┐
    #> │ values           ┆ unique           │
    #> │ ---              ┆ ---              │
    #> │ array[f64, 3]    ┆ list[f64]        │
    #> ╞══════════════════╪══════════════════╡
    #> │ [1.0, 1.0, 2.0]  ┆ [1.0, 2.0]       │
    #> │ [4.0, 4.0, 4.0]  ┆ [4.0]            │
    #> │ [null, 6.0, 7.0] ┆ [null, 6.0, 7.0] │
    #> └──────────────────┴──────────────────┘
