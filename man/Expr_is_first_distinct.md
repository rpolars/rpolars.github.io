

# Check whether each value is the first occurrence

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/after-wrappers.R#L20)

## Description

Check whether each value is the first occurrence

## Usage

<pre><code class='language-R'>Expr_is_first_distinct()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(head(mtcars[, 1:2]))$
  with_columns(is_ufirst = pl$col("mpg")$is_first_distinct())
```

    #> shape: (6, 3)
    #> ┌──────┬─────┬───────────┐
    #> │ mpg  ┆ cyl ┆ is_ufirst │
    #> │ ---  ┆ --- ┆ ---       │
    #> │ f64  ┆ f64 ┆ bool      │
    #> ╞══════╪═════╪═══════════╡
    #> │ 21.0 ┆ 6.0 ┆ true      │
    #> │ 21.0 ┆ 6.0 ┆ false     │
    #> │ 22.8 ┆ 4.0 ┆ true      │
    #> │ 21.4 ┆ 6.0 ┆ true      │
    #> │ 18.7 ┆ 8.0 ┆ true      │
    #> │ 18.1 ┆ 6.0 ┆ true      │
    #> └──────┴─────┴───────────┘
