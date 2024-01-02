
# Check if elements are not NaN

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/#L)

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
