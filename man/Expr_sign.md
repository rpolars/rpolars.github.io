

# Get the sign of elements

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/after-wrappers.R#L20)

## Description

Get the sign of elements

## Usage

<pre><code class='language-R'>Expr_sign()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = c(.9, -3, -0, 0, 4, NA_real_))$
  with_columns(sign = pl$col("a")$sign())
```

    #> shape: (6, 2)
    #> ┌──────┬──────┐
    #> │ a    ┆ sign │
    #> │ ---  ┆ ---  │
    #> │ f64  ┆ i64  │
    #> ╞══════╪══════╡
    #> │ 0.9  ┆ 1    │
    #> │ -3.0 ┆ -1   │
    #> │ -0.0 ┆ 0    │
    #> │ 0.0  ┆ 0    │
    #> │ 4.0  ┆ 1    │
    #> │ null ┆ null │
    #> └──────┴──────┘
