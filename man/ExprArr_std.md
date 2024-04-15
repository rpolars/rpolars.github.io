

# Find the standard deviation in an array

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/expr__array.R#L78)

## Description

Find the standard deviation in an array

## Usage

<pre><code class='language-R'>ExprArr_std(ddof = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprArr_std_:_ddof">ddof</code>
</td>
<td>
Delta Degrees of Freedom: the divisor used in the calculation is N -
ddof, where N represents the number of elements. By default ddof is 1.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  values = list(c(2, 1, 4), c(8.4, 3.2, 1)),
  schema = list(values = pl$Array(pl$Float64, 3))
)
df$with_columns(std = pl$col("values")$arr$std())
```

    #> shape: (2, 2)
    #> ┌─────────────────┬──────────┐
    #> │ values          ┆ std      │
    #> │ ---             ┆ ---      │
    #> │ array[f64, 3]   ┆ f64      │
    #> ╞═════════════════╪══════════╡
    #> │ [2.0, 1.0, 4.0] ┆ 1.527525 │
    #> │ [8.4, 3.2, 1.0] ┆ 3.8      │
    #> └─────────────────┴──────────┘
