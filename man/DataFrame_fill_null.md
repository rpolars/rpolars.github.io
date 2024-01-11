
# Fill nulls

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L1209)

## Description

Fill null values (which correspond to <code>NA</code> in R) using the
specified value or strategy.

## Usage

<pre><code class='language-R'>DataFrame_fill_null(fill_value)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_fill_null_:_fill_value">fill_value</code>
</td>
<td>
Value to fill nulls with.
</td>
</tr>
</table>

## Value

DataFrame

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = c(1.5, 2, NA, 4),
  b = c(1.5, NA, NA, 4)
)

df$fill_null(99)
```

    #> shape: (4, 2)
    #> ┌──────┬──────┐
    #> │ a    ┆ b    │
    #> │ ---  ┆ ---  │
    #> │ f64  ┆ f64  │
    #> ╞══════╪══════╡
    #> │ 1.5  ┆ 1.5  │
    #> │ 2.0  ┆ 99.0 │
    #> │ 99.0 ┆ 99.0 │
    #> │ 4.0  ┆ 4.0  │
    #> └──────┴──────┘

``` r
df$fill_null(pl$col("a")$mean())
```

    #> shape: (4, 2)
    #> ┌─────┬─────┐
    #> │ a   ┆ b   │
    #> │ --- ┆ --- │
    #> │ f64 ┆ f64 │
    #> ╞═════╪═════╡
    #> │ 1.5 ┆ 1.5 │
    #> │ 2.0 ┆ 2.5 │
    #> │ 2.5 ┆ 2.5 │
    #> │ 4.0 ┆ 4.0 │
    #> └─────┴─────┘
