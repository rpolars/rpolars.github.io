

# Var

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L891)

## Description

Aggregate the columns of this LazyFrame to their variance values.

## Usage

<pre><code class='language-R'>LazyFrame_var(ddof = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_var_:_ddof">ddof</code>
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

pl$LazyFrame(mtcars)$var()$collect()
```

    #> shape: (1, 11)
    #> ┌───────────┬──────────┬─────────────┬─────────────┬───┬──────────┬──────────┬──────────┬──────────┐
    #> │ mpg       ┆ cyl      ┆ disp        ┆ hp          ┆ … ┆ vs       ┆ am       ┆ gear     ┆ carb     │
    #> │ ---       ┆ ---      ┆ ---         ┆ ---         ┆   ┆ ---      ┆ ---      ┆ ---      ┆ ---      │
    #> │ f64       ┆ f64      ┆ f64         ┆ f64         ┆   ┆ f64      ┆ f64      ┆ f64      ┆ f64      │
    #> ╞═══════════╪══════════╪═════════════╪═════════════╪═══╪══════════╪══════════╪══════════╪══════════╡
    #> │ 36.324103 ┆ 3.189516 ┆ 15360.79982 ┆ 4700.866935 ┆ … ┆ 0.254032 ┆ 0.248992 ┆ 0.544355 ┆ 2.608871 │
    #> │           ┆          ┆ 9           ┆             ┆   ┆          ┆          ┆          ┆          │
    #> └───────────┴──────────┴─────────────┴─────────────┴───┴──────────┴──────────┴──────────┴──────────┘
