

# Std

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L894)

## Description

Aggregate the columns of this LazyFrame to their standard deviation
values.

## Usage

<pre><code class='language-R'>LazyFrame_std(ddof = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_std_:_ddof">ddof</code>
</td>
<td>
Delta Degrees of Freedom: the divisor used in the calculation is N -
ddof, where N represents the number of elements. By default ddof is 1.
</td>
</tr>
</table>

## Value

A LazyFrame with one row

## Examples

``` r
library(polars)

pl$LazyFrame(mtcars)$std()$collect()
```

    #> shape: (1, 11)
    #> ┌──────────┬──────────┬────────────┬───────────┬───┬──────────┬──────────┬──────────┬────────┐
    #> │ mpg      ┆ cyl      ┆ disp       ┆ hp        ┆ … ┆ vs       ┆ am       ┆ gear     ┆ carb   │
    #> │ ---      ┆ ---      ┆ ---        ┆ ---       ┆   ┆ ---      ┆ ---      ┆ ---      ┆ ---    │
    #> │ f64      ┆ f64      ┆ f64        ┆ f64       ┆   ┆ f64      ┆ f64      ┆ f64      ┆ f64    │
    #> ╞══════════╪══════════╪════════════╪═══════════╪═══╪══════════╪══════════╪══════════╪════════╡
    #> │ 6.026948 ┆ 1.785922 ┆ 123.938694 ┆ 68.562868 ┆ … ┆ 0.504016 ┆ 0.498991 ┆ 0.737804 ┆ 1.6152 │
    #> └──────────┴──────────┴────────────┴───────────┴───┴──────────┴──────────┴──────────┴────────┘
