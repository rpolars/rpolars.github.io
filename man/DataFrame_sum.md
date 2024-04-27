

# Sum

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/dataframe__frame.R#L1288)

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
