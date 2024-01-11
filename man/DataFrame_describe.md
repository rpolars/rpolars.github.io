
# Summary statistics for a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L1467)

## Description

This returns the total number of rows, the number of missing values, the
mean, standard deviation, min, max, median and the percentiles specified
in the argument <code>percentiles</code>.

## Usage

<pre><code class='language-R'>DataFrame_describe(percentiles = c(0.25, 0.75))
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_describe_:_percentiles">percentiles</code>
</td>
<td>
One or more percentiles to include in the summary statistics. All values
must be in the range <code style="white-space: pre;">\[0; 1\]</code>.
</td>
</tr>
</table>

## Value

DataFrame

## Examples

``` r
library(polars)

pl$DataFrame(mtcars)$describe()
```

    #> shape: (9, 12)
    #> ┌────────────┬───────────┬──────────┬────────────┬───┬──────────┬──────────┬──────────┬────────┐
    #> │ describe   ┆ mpg       ┆ cyl      ┆ disp       ┆ … ┆ vs       ┆ am       ┆ gear     ┆ carb   │
    #> │ ---        ┆ ---       ┆ ---      ┆ ---        ┆   ┆ ---      ┆ ---      ┆ ---      ┆ ---    │
    #> │ str        ┆ f64       ┆ f64      ┆ f64        ┆   ┆ f64      ┆ f64      ┆ f64      ┆ f64    │
    #> ╞════════════╪═══════════╪══════════╪════════════╪═══╪══════════╪══════════╪══════════╪════════╡
    #> │ count      ┆ 32.0      ┆ 32.0     ┆ 32.0       ┆ … ┆ 32.0     ┆ 32.0     ┆ 32.0     ┆ 32.0   │
    #> │ null_count ┆ 0.0       ┆ 0.0      ┆ 0.0        ┆ … ┆ 0.0      ┆ 0.0      ┆ 0.0      ┆ 0.0    │
    #> │ mean       ┆ 20.090625 ┆ 6.1875   ┆ 230.721875 ┆ … ┆ 0.4375   ┆ 0.40625  ┆ 3.6875   ┆ 2.8125 │
    #> │ std        ┆ 6.026948  ┆ 1.785922 ┆ 123.938694 ┆ … ┆ 0.504016 ┆ 0.498991 ┆ 0.737804 ┆ 1.6152 │
    #> │ min        ┆ 10.4      ┆ 4.0      ┆ 71.1       ┆ … ┆ 0.0      ┆ 0.0      ┆ 3.0      ┆ 1.0    │
    #> │ max        ┆ 33.9      ┆ 8.0      ┆ 472.0      ┆ … ┆ 1.0      ┆ 1.0      ┆ 5.0      ┆ 8.0    │
    #> │ median     ┆ 19.2      ┆ 6.0      ┆ 196.3      ┆ … ┆ 0.0      ┆ 0.0      ┆ 4.0      ┆ 2.0    │
    #> │ 25pct      ┆ 15.5      ┆ 4.0      ┆ 121.0      ┆ … ┆ 0.0      ┆ 0.0      ┆ 3.0      ┆ 2.0    │
    #> │ 75pct      ┆ 22.8      ┆ 8.0      ┆ 318.0      ┆ … ┆ 1.0      ┆ 1.0      ┆ 4.0      ┆ 4.0    │
    #> └────────────┴───────────┴──────────┴────────────┴───┴──────────┴──────────┴──────────┴────────┘
