

# Median

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/lazyframe__lazy.R#L859)

## Description

Aggregate the columns in the LazyFrame to their median value.

## Usage

<pre><code class='language-R'>LazyFrame_median()
</code></pre>

## Value

A LazyFrame with one row

## Examples

``` r
library(polars)

pl$LazyFrame(mtcars)$median()$collect()
```

    #> shape: (1, 11)
    #> ┌──────┬─────┬───────┬───────┬───┬─────┬─────┬──────┬──────┐
    #> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
    #> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
    #> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
    #> ╞══════╪═════╪═══════╪═══════╪═══╪═════╪═════╪══════╪══════╡
    #> │ 19.2 ┆ 6.0 ┆ 196.3 ┆ 123.0 ┆ … ┆ 0.0 ┆ 0.0 ┆ 4.0  ┆ 2.0  │
    #> └──────┴─────┴───────┴───────┴───┴─────┴─────┴──────┴──────┘
