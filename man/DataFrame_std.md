
# Std

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/dataframe__frame.R#L1154)

## Description

Aggregate the columns of this DataFrame to their standard deviation
values.

## Usage

<pre><code class='language-R'>DataFrame_std(ddof = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_std_:_ddof">ddof</code>
</td>
<td>
Delta Degrees of Freedom: the divisor used in the calculation is N -
ddof, where N represents the number of elements. By default ddof is 1.
</td>
</tr>
</table>

## Value

A DataFrame with one row.

## Examples

``` r
library(polars)

pl$DataFrame(mtcars)$std()
```

    #> shape: (1, 11)
    #> ┌──────────┬──────────┬────────────┬───────────┬───┬──────────┬──────────┬──────────┬────────┐
    #> │ mpg      ┆ cyl      ┆ disp       ┆ hp        ┆ … ┆ vs       ┆ am       ┆ gear     ┆ carb   │
    #> │ ---      ┆ ---      ┆ ---        ┆ ---       ┆   ┆ ---      ┆ ---      ┆ ---      ┆ ---    │
    #> │ f64      ┆ f64      ┆ f64        ┆ f64       ┆   ┆ f64      ┆ f64      ┆ f64      ┆ f64    │
    #> ╞══════════╪══════════╪════════════╪═══════════╪═══╪══════════╪══════════╪══════════╪════════╡
    #> │ 6.026948 ┆ 1.785922 ┆ 123.938694 ┆ 68.562868 ┆ … ┆ 0.504016 ┆ 0.498991 ┆ 0.737804 ┆ 1.6152 │
    #> └──────────┴──────────┴────────────┴───────────┴───┴──────────┴──────────┴──────────┴────────┘
