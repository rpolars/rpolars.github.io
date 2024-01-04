
# Sum

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/dataframe__frame.R#L1129)

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
