
# Min

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L861)

## Description

Aggregate the columns in the LazyFrame to their minimum value.

## Usage

<pre><code class='language-R'>LazyFrame_min()
</code></pre>

## Value

A LazyFrame with one row

## Examples

``` r
library(polars)

pl$LazyFrame(mtcars)$min()$collect()
```

    #> shape: (1, 11)
    #> ┌──────┬─────┬──────┬──────┬───┬─────┬─────┬──────┬──────┐
    #> │ mpg  ┆ cyl ┆ disp ┆ hp   ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
    #> │ ---  ┆ --- ┆ ---  ┆ ---  ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
    #> │ f64  ┆ f64 ┆ f64  ┆ f64  ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
    #> ╞══════╪═════╪══════╪══════╪═══╪═════╪═════╪══════╪══════╡
    #> │ 10.4 ┆ 4.0 ┆ 71.1 ┆ 52.0 ┆ … ┆ 0.0 ┆ 0.0 ┆ 3.0  ┆ 1.0  │
    #> └──────┴─────┴──────┴──────┴───┴─────┴─────┴──────┴──────┘
