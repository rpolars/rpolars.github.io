
# Mean

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/lazyframe__lazy.R#L777)

## Description

Aggregate the columns in the LazyFrame to their mean value.

## Usage

<pre><code class='language-R'>LazyFrame_mean()
</code></pre>

## Value

A LazyFrame with one row

## Examples

``` r
library(polars)

pl$LazyFrame(mtcars)$mean()$collect()
```

    #> shape: (1, 11)
    #> ┌───────────┬────────┬────────────┬──────────┬───┬────────┬─────────┬────────┬────────┐
    #> │ mpg       ┆ cyl    ┆ disp       ┆ hp       ┆ … ┆ vs     ┆ am      ┆ gear   ┆ carb   │
    #> │ ---       ┆ ---    ┆ ---        ┆ ---      ┆   ┆ ---    ┆ ---     ┆ ---    ┆ ---    │
    #> │ f64       ┆ f64    ┆ f64        ┆ f64      ┆   ┆ f64    ┆ f64     ┆ f64    ┆ f64    │
    #> ╞═══════════╪════════╪════════════╪══════════╪═══╪════════╪═════════╪════════╪════════╡
    #> │ 20.090625 ┆ 6.1875 ┆ 230.721875 ┆ 146.6875 ┆ … ┆ 0.4375 ┆ 0.40625 ┆ 3.6875 ┆ 2.8125 │
    #> └───────────┴────────┴────────────┴──────────┴───┴────────┴─────────┴────────┴────────┘
