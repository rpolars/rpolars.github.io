
# Get median value

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/#L)

## Description

Get median value

## Usage

<pre><code class='language-R'>Expr_median
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(x = c(1L, NA, 2L))$
  with_columns(median = pl$col("x")$median())
```

    #> shape: (3, 2)
    #> ┌──────┬────────┐
    #> │ x    ┆ median │
    #> │ ---  ┆ ---    │
    #> │ i32  ┆ f64    │
    #> ╞══════╪════════╡
    #> │ 1    ┆ 1.5    │
    #> │ null ┆ 1.5    │
    #> │ 2    ┆ 1.5    │
    #> └──────┴────────┘
