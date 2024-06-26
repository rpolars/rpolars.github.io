

# Shift

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/group_by.R#L281)

## Description

Shift the values by a given period.

## Usage

<pre><code class='language-R'>GroupBy_shift(periods = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="periods">periods</code>
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

pl$DataFrame(mtcars)$group_by("cyl")$shift(2)
```

    #> shape: (3, 11)
    #> ┌─────┬────────────┬────────────┬────────────┬───┬────────────┬────────────┬───────────┬───────────┐
    #> │ cyl ┆ mpg        ┆ disp       ┆ hp         ┆ … ┆ vs         ┆ am         ┆ gear      ┆ carb      │
    #> │ --- ┆ ---        ┆ ---        ┆ ---        ┆   ┆ ---        ┆ ---        ┆ ---       ┆ ---       │
    #> │ f64 ┆ list[f64]  ┆ list[f64]  ┆ list[f64]  ┆   ┆ list[f64]  ┆ list[f64]  ┆ list[f64] ┆ list[f64] │
    #> ╞═════╪════════════╪════════════╪════════════╪═══╪════════════╪════════════╪═══════════╪═══════════╡
    #> │ 8.0 ┆ [null,     ┆ [null,     ┆ [null,     ┆ … ┆ [null,     ┆ [null,     ┆ [null,    ┆ [null,    │
    #> │     ┆ null, …    ┆ null, …    ┆ null, …    ┆   ┆ null, …    ┆ null, …    ┆ null, …   ┆ null, …   │
    #> │     ┆ 19.2]      ┆ 400.0]     ┆ 175.0]     ┆   ┆ 0.0]       ┆ 0.0]       ┆ 3.0]      ┆ 2.0]      │
    #> │ 6.0 ┆ [null,     ┆ [null,     ┆ [null,     ┆ … ┆ [null,     ┆ [null,     ┆ [null,    ┆ [null,    │
    #> │     ┆ null, …    ┆ null, …    ┆ null, …    ┆   ┆ null, …    ┆ null, …    ┆ null, …   ┆ null, …   │
    #> │     ┆ 19.2]      ┆ 167.6]     ┆ 123.0]     ┆   ┆ 1.0]       ┆ 0.0]       ┆ 4.0]      ┆ 4.0]      │
    #> │ 4.0 ┆ [null,     ┆ [null,     ┆ [null,     ┆ … ┆ [null,     ┆ [null,     ┆ [null,    ┆ [null,    │
    #> │     ┆ null, …    ┆ null, …    ┆ null, …    ┆   ┆ null, …    ┆ null, …    ┆ null, …   ┆ null, …   │
    #> │     ┆ 26.0]      ┆ 120.3]     ┆ 91.0]      ┆   ┆ 0.0]       ┆ 1.0]       ┆ 5.0]      ┆ 2.0]      │
    #> └─────┴────────────┴────────────┴────────────┴───┴────────────┴────────────┴───────────┴───────────┘
