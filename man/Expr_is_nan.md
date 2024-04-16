

# Check if elements are NaN

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/after-wrappers.R#L20)

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
