

# Shift

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L943)

## Description

Shift the values by a given period.

## Usage

<pre><code class='language-R'>LazyFrame_shift(periods = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_shift_:_periods">periods</code>
</td>
<td>
integer Number of periods to shift (may be negative).
</td>
</tr>
</table>

## Value

LazyFrame

## Examples

``` r
library(polars)

pl$LazyFrame(mtcars)$shift(2)$collect()
```

    #> shape: (32, 11)
    #> ┌──────┬──────┬───────┬───────┬───┬──────┬──────┬──────┬──────┐
    #> │ mpg  ┆ cyl  ┆ disp  ┆ hp    ┆ … ┆ vs   ┆ am   ┆ gear ┆ carb │
    #> │ ---  ┆ ---  ┆ ---   ┆ ---   ┆   ┆ ---  ┆ ---  ┆ ---  ┆ ---  │
    #> │ f64  ┆ f64  ┆ f64   ┆ f64   ┆   ┆ f64  ┆ f64  ┆ f64  ┆ f64  │
    #> ╞══════╪══════╪═══════╪═══════╪═══╪══════╪══════╪══════╪══════╡
    #> │ null ┆ null ┆ null  ┆ null  ┆ … ┆ null ┆ null ┆ null ┆ null │
    #> │ null ┆ null ┆ null  ┆ null  ┆ … ┆ null ┆ null ┆ null ┆ null │
    #> │ 21.0 ┆ 6.0  ┆ 160.0 ┆ 110.0 ┆ … ┆ 0.0  ┆ 1.0  ┆ 4.0  ┆ 4.0  │
    #> │ 21.0 ┆ 6.0  ┆ 160.0 ┆ 110.0 ┆ … ┆ 0.0  ┆ 1.0  ┆ 4.0  ┆ 4.0  │
    #> │ 22.8 ┆ 4.0  ┆ 108.0 ┆ 93.0  ┆ … ┆ 1.0  ┆ 1.0  ┆ 4.0  ┆ 1.0  │
    #> │ …    ┆ …    ┆ …     ┆ …     ┆ … ┆ …    ┆ …    ┆ …    ┆ …    │
    #> │ 27.3 ┆ 4.0  ┆ 79.0  ┆ 66.0  ┆ … ┆ 1.0  ┆ 1.0  ┆ 4.0  ┆ 1.0  │
    #> │ 26.0 ┆ 4.0  ┆ 120.3 ┆ 91.0  ┆ … ┆ 0.0  ┆ 1.0  ┆ 5.0  ┆ 2.0  │
    #> │ 30.4 ┆ 4.0  ┆ 95.1  ┆ 113.0 ┆ … ┆ 1.0  ┆ 1.0  ┆ 5.0  ┆ 2.0  │
    #> │ 15.8 ┆ 8.0  ┆ 351.0 ┆ 264.0 ┆ … ┆ 0.0  ┆ 1.0  ┆ 5.0  ┆ 4.0  │
    #> │ 19.7 ┆ 6.0  ┆ 145.0 ┆ 175.0 ┆ … ┆ 0.0  ┆ 1.0  ┆ 5.0  ┆ 6.0  │
    #> └──────┴──────┴───────┴───────┴───┴──────┴──────┴──────┴──────┘
