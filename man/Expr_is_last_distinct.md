

# Check whether each value is the last occurrence

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/after-wrappers.R#L20)

## Description

Check whether each value is the last occurrence

## Usage

<pre><code class='language-R'>Expr_is_last_distinct()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(head(mtcars[, 1:2]))$
  with_columns(is_ulast = pl$col("mpg")$is_last_distinct())
```

    #> shape: (6, 3)
    #> ┌──────┬─────┬──────────┐
    #> │ mpg  ┆ cyl ┆ is_ulast │
    #> │ ---  ┆ --- ┆ ---      │
    #> │ f64  ┆ f64 ┆ bool     │
    #> ╞══════╪═════╪══════════╡
    #> │ 21.0 ┆ 6.0 ┆ false    │
    #> │ 21.0 ┆ 6.0 ┆ true     │
    #> │ 22.8 ┆ 4.0 ┆ true     │
    #> │ 21.4 ┆ 6.0 ┆ true     │
    #> │ 18.7 ┆ 8.0 ┆ true     │
    #> │ 18.1 ┆ 6.0 ┆ true     │
    #> └──────┴─────┴──────────┘
