
# Fill <code>NaN</code>

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/lazyframe__lazy.R#L854)

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
