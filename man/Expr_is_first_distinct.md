
# Check whether each value is the first occurrence

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/#L)

## Description

Check whether each value is the first occurrence

## Usage

<pre><code class='language-R'>Expr_is_first_distinct
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
