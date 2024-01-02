
# Check if elements are NaN

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/#L)

## Description

Returns a boolean Series indicating which values are NaN.

## Usage

<pre><code class='language-R'>Expr_is_nan
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(list(alice = c(0, NaN, NA, Inf, -Inf)))$
  with_columns(nan = pl$col("alice")$is_nan())
```

    #> shape: (5, 2)
    #> ┌───────┬───────┐
    #> │ alice ┆ nan   │
    #> │ ---   ┆ ---   │
    #> │ f64   ┆ bool  │
    #> ╞═══════╪═══════╡
    #> │ 0.0   ┆ false │
    #> │ NaN   ┆ true  │
    #> │ null  ┆ null  │
    #> │ inf   ┆ false │
    #> │ -inf  ┆ false │
    #> └───────┴───────┘
