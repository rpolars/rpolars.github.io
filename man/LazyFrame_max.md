
# Max

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/lazyframe__lazy.R#L766)

## Description

Aggregate the columns in the LazyFrame to their maximum value.

## Usage

<pre><code class='language-R'>LazyFrame_max()
</code></pre>

## Value

A LazyFrame with one row

## Examples

``` r
library(polars)

pl$LazyFrame(mtcars)$max()$collect()
```

    #> shape: (1, 11)
    #> ┌──────┬─────┬───────┬───────┬───┬─────┬─────┬──────┬──────┐
    #> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
    #> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
    #> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
    #> ╞══════╪═════╪═══════╪═══════╪═══╪═════╪═════╪══════╪══════╡
    #> │ 33.9 ┆ 8.0 ┆ 472.0 ┆ 335.0 ┆ … ┆ 1.0 ┆ 1.0 ┆ 5.0  ┆ 8.0  │
    #> └──────┴─────┴───────┴───────┴───┴─────┴─────┴──────┴──────┘
