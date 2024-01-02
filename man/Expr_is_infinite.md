
# Check if elements are infinite

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/#L)

## Description

Returns a boolean Series indicating which values are infinite.

## Usage

<pre><code class='language-R'>Expr_is_infinite
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(list(alice = c(0, NaN, NA, Inf, -Inf)))$
  with_columns(infinite = pl$col("alice")$is_infinite())
```

    #> shape: (5, 2)
    #> ┌───────┬──────────┐
    #> │ alice ┆ infinite │
    #> │ ---   ┆ ---      │
    #> │ f64   ┆ bool     │
    #> ╞═══════╪══════════╡
    #> │ 0.0   ┆ false    │
    #> │ NaN   ┆ false    │
    #> │ null  ┆ null     │
    #> │ inf   ┆ true     │
    #> │ -inf  ┆ true     │
    #> └───────┴──────────┘
