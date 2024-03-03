

# Get mean value

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/after-wrappers.R#L20)

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
