
# Get mean value

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/#L)

## Description

Get mean value

## Usage

<pre><code class='language-R'>Expr_mean
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
