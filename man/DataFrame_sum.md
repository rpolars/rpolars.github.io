
# Sum

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/dataframe__frame.R#L1131)

## Description

Aggregate the columns of this DataFrame to their sum values.

## Usage

<pre><code class='language-R'>DataFrame_sum()
</code></pre>

## Value

A DataFrame with one row.

## Examples

``` r
library(polars)

pl$DataFrame(mtcars)$sum()
```

    #> shape: (1, 11)
    #> ┌───────┬───────┬────────┬────────┬───┬──────┬──────┬───────┬──────┐
    #> │ mpg   ┆ cyl   ┆ disp   ┆ hp     ┆ … ┆ vs   ┆ am   ┆ gear  ┆ carb │
    #> │ ---   ┆ ---   ┆ ---    ┆ ---    ┆   ┆ ---  ┆ ---  ┆ ---   ┆ ---  │
    #> │ f64   ┆ f64   ┆ f64    ┆ f64    ┆   ┆ f64  ┆ f64  ┆ f64   ┆ f64  │
    #> ╞═══════╪═══════╪════════╪════════╪═══╪══════╪══════╪═══════╪══════╡
    #> │ 642.9 ┆ 198.0 ┆ 7383.1 ┆ 4694.0 ┆ … ┆ 14.0 ┆ 13.0 ┆ 118.0 ┆ 90.0 │
    #> └───────┴───────┴────────┴────────┴───┴──────┴──────┴───────┴──────┘
