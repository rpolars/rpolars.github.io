

# Fill <code>NaN</code>

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L1276)

## Description

Fill <code>NaN</code> values by an Expression evaluation.

## Usage

<pre><code class='language-R'>DataFrame_fill_nan(fill_value)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_fill_nan_:_fill_value">fill_value</code>
</td>
<td>
Value to fill <code>NaN</code> with.
</td>
</tr>
</table>

## Value

DataFrame

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = c(1.5, 2, NaN, 4),
  b = c(1.5, NaN, NaN, 4)
)
df$fill_nan(99)
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
