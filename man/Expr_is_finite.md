

# Check if elements are finite

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/after-wrappers.R#L20)

## Description

Returns a boolean Series indicating which values are finite.

## Usage

<pre><code class='language-R'>Expr_is_finite()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(list(alice = c(0, NaN, NA, Inf, -Inf)))$
  with_columns(finite = pl$col("alice")$is_finite())
```

    #> shape: (5, 2)
    #> ┌───────┬────────┐
    #> │ alice ┆ finite │
    #> │ ---   ┆ ---    │
    #> │ f64   ┆ bool   │
    #> ╞═══════╪════════╡
    #> │ 0.0   ┆ true   │
    #> │ NaN   ┆ false  │
    #> │ null  ┆ null   │
    #> │ inf   ┆ false  │
    #> │ -inf  ┆ false  │
    #> └───────┴────────┘
