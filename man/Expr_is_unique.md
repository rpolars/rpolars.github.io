

# Check whether each value is unique

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/after-wrappers.R#L20)

## Description

Check whether each value is unique

## Usage

<pre><code class='language-R'>Expr_is_unique()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(head(mtcars[, 1:2]))$
  with_columns(is_unique = pl$col("mpg")$is_unique())
```

    #> shape: (6, 3)
    #> ┌──────┬─────┬───────────┐
    #> │ mpg  ┆ cyl ┆ is_unique │
    #> │ ---  ┆ --- ┆ ---       │
    #> │ f64  ┆ f64 ┆ bool      │
    #> ╞══════╪═════╪═══════════╡
    #> │ 21.0 ┆ 6.0 ┆ false     │
    #> │ 21.0 ┆ 6.0 ┆ false     │
    #> │ 22.8 ┆ 4.0 ┆ true      │
    #> │ 21.4 ┆ 6.0 ┆ true      │
    #> │ 18.7 ┆ 8.0 ┆ true      │
    #> │ 18.1 ┆ 6.0 ┆ true      │
    #> └──────┴─────┴───────────┘
