

# Sum

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/lazyframe__lazy.R#L866)

## Description

Aggregate the columns of this LazyFrame to their sum values.

## Usage

<pre><code class='language-R'>LazyFrame_sum()
</code></pre>

## Value

A LazyFrame with one row

## Examples

``` r
library(polars)

pl$LazyFrame(mtcars)$sum()$collect()
```

    #> shape: (1, 11)
    #> ┌───────┬───────┬────────┬────────┬───┬──────┬──────┬───────┬──────┐
    #> │ mpg   ┆ cyl   ┆ disp   ┆ hp     ┆ … ┆ vs   ┆ am   ┆ gear  ┆ carb │
    #> │ ---   ┆ ---   ┆ ---    ┆ ---    ┆   ┆ ---  ┆ ---  ┆ ---   ┆ ---  │
    #> │ f64   ┆ f64   ┆ f64    ┆ f64    ┆   ┆ f64  ┆ f64  ┆ f64   ┆ f64  │
    #> ╞═══════╪═══════╪════════╪════════╪═══╪══════╪══════╪═══════╪══════╡
    #> │ 642.9 ┆ 198.0 ┆ 7383.1 ┆ 4694.0 ┆ … ┆ 14.0 ┆ 13.0 ┆ 118.0 ┆ 90.0 │
    #> └───────┴───────┴────────┴────────┴───┴──────┴──────┴───────┴──────┘
