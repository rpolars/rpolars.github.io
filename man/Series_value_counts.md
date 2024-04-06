

# Count the occurrences of unique values

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L587)

## Description

Count the occurrences of unique values

## Usage

<pre><code class='language-R'>Series_value_counts(sort = TRUE, parallel = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_value_counts_:_sort">sort</code>
</td>
<td>
Ensure the output is sorted from most values to least.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_value_counts_:_parallel">parallel</code>
</td>
<td>
Better to turn this off in the aggregation context, as it can lead to
contention.
</td>
</tr>
</table>

## Value

DataFrame

## Examples

``` r
library(polars)

as_polars_series(iris$Species, name = "flower species")$value_counts()
```

    #> shape: (3, 2)
    #> ┌────────────────┬───────┐
    #> │ flower species ┆ count │
    #> │ ---            ┆ ---   │
    #> │ cat            ┆ u32   │
    #> ╞════════════════╪═══════╡
    #> │ setosa         ┆ 50    │
    #> │ versicolor     ┆ 50    │
    #> │ virginica      ┆ 50    │
    #> └────────────────┴───────┘
