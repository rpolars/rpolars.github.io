
# Check if elements are not NaN

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/#L)

## Description

Returns a boolean Series indicating which values are not NaN. Syntactic
sugar for <code style="white-space: pre;">$is_nan()$not()</code>.

## Usage

<pre><code class='language-R'>Expr_is_not_nan
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(list(alice = c(0, NaN, NA, Inf, -Inf)))$
  with_columns(not_nan = pl$col("alice")$is_not_nan())
```

    #> shape: (5, 2)
    #> ┌───────┬─────────┐
    #> │ alice ┆ not_nan │
    #> │ ---   ┆ ---     │
    #> │ f64   ┆ bool    │
    #> ╞═══════╪═════════╡
    #> │ 0.0   ┆ true    │
    #> │ NaN   ┆ false   │
    #> │ null  ┆ true    │
    #> │ inf   ┆ true    │
    #> │ -inf  ┆ true    │
    #> └───────┴─────────┘
