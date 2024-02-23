

# Check if elements are NaN

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/after-wrappers.R#L20)

## Description

Returns a boolean Series indicating which values are NaN.

## Usage

<pre><code class='language-R'>Expr_is_nan()
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
