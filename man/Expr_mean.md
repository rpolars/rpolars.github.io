

# Get mean value

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/after-wrappers.R#L20)

## Description

Get mean value

## Usage

<pre><code class='language-R'>Expr_mean()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(x = c(1L, NA, 2L))$
  with_columns(mean = pl$col("x")$mean())
```

    #> shape: (3, 2)
    #> ┌──────┬──────┐
    #> │ x    ┆ mean │
    #> │ ---  ┆ ---  │
    #> │ i32  ┆ f64  │
    #> ╞══════╪══════╡
    #> │ 1    ┆ 1.5  │
    #> │ null ┆ 1.5  │
    #> │ 2    ┆ 1.5  │
    #> └──────┴──────┘
