
# Shift and fill

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/group_by.R#L271)

## Description

Shift and fill the values by a given period.

## Usage

<pre><code class='language-R'>GroupBy_shift_and_fill(fill_value, periods = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="GroupBy_shift_and_fill_:_fill_value">fill_value</code>
</td>
<td>
fill None values with the result of this expression.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="GroupBy_shift_and_fill_:_periods">periods</code>
</td>
<td>
integer Number of periods to shift (may be negative).
</td>
</tr>
</table>

## Value

GroupBy

## Examples

``` r
library(polars)

pl$DataFrame(mtcars)$group_by("cyl")$shift_and_fill(99, 1)
```

    #> shape: (3, 11)
    #> ┌─────┬────────────┬────────────┬────────────┬───┬────────────┬────────────┬───────────┬───────────┐
    #> │ cyl ┆ mpg        ┆ disp       ┆ hp         ┆ … ┆ vs         ┆ am         ┆ gear      ┆ carb      │
    #> │ --- ┆ ---        ┆ ---        ┆ ---        ┆   ┆ ---        ┆ ---        ┆ ---       ┆ ---       │
    #> │ f64 ┆ list[f64]  ┆ list[f64]  ┆ list[f64]  ┆   ┆ list[f64]  ┆ list[f64]  ┆ list[f64] ┆ list[f64] │
    #> ╞═════╪════════════╪════════════╪════════════╪═══╪════════════╪════════════╪═══════════╪═══════════╡
    #> │ 4.0 ┆ [99.0,     ┆ [99.0,     ┆ [99.0,     ┆ … ┆ [99.0,     ┆ [99.0,     ┆ [99.0,    ┆ [99.0,    │
    #> │     ┆ 22.8, …    ┆ 108.0, …   ┆ 93.0, …    ┆   ┆ 1.0, …     ┆ 1.0, …     ┆ 4.0, …    ┆ 1.0, …    │
    #> │     ┆ 30.4]      ┆ 95.1]      ┆ 113.0]     ┆   ┆ 1.0]       ┆ 1.0]       ┆ 5.0]      ┆ 2.0]      │
    #> │ 6.0 ┆ [99.0,     ┆ [99.0,     ┆ [99.0,     ┆ … ┆ [99.0,     ┆ [99.0,     ┆ [99.0,    ┆ [99.0,    │
    #> │     ┆ 21.0, …    ┆ 160.0, …   ┆ 110.0, …   ┆   ┆ 0.0, …     ┆ 1.0, …     ┆ 4.0, …    ┆ 4.0, …    │
    #> │     ┆ 17.8]      ┆ 167.6]     ┆ 123.0]     ┆   ┆ 1.0]       ┆ 0.0]       ┆ 4.0]      ┆ 4.0]      │
    #> │ 8.0 ┆ [99.0,     ┆ [99.0,     ┆ [99.0,     ┆ … ┆ [99.0,     ┆ [99.0,     ┆ [99.0,    ┆ [99.0,    │
    #> │     ┆ 18.7, …    ┆ 360.0, …   ┆ 175.0, …   ┆   ┆ 0.0, …     ┆ 0.0, …     ┆ 3.0, …    ┆ 2.0, …    │
    #> │     ┆ 15.8]      ┆ 351.0]     ┆ 264.0]     ┆   ┆ 0.0]       ┆ 1.0]       ┆ 5.0]      ┆ 4.0]      │
    #> └─────┴────────────┴────────────┴────────────┴───┴────────────┴────────────┴───────────┴───────────┘
