

# Fill <code>NaN</code>

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/lazyframe__lazy.R#L910)

## Description

Fill <code>NaN</code> values by an Expression evaluation.

## Usage

<pre><code class='language-R'>LazyFrame_fill_nan(fill_value)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_fill_nan_:_fill_value">fill_value</code>
</td>
<td>
Value to fill <code>NaN</code> with.
</td>
</tr>
</table>

## Value

LazyFrame

## Examples

``` r
library(polars)

df = pl$LazyFrame(
  a = c(1.5, 2, NaN, 4),
  b = c(1.5, NaN, NaN, 4)
)
df$fill_nan(99)$collect()
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
