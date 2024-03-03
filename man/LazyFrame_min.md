

# Min

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/lazyframe__lazy.R#L930)

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
