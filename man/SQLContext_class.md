

# Run SQL queries against DataFrame/LazyFrame data.

## Description

Run SQL queries against DataFrame/LazyFrame data.

## Details

Currently, only available when built with the "sql" feature. See
polars_info for more information.

## Examples

``` r
library(polars)


lf = pl$LazyFrame(a = 1:3, b = c("x", NA, "z"))
res = pl$SQLContext(frame = lf)$execute(
  "SELECT b, a*2 AS two_a FROM frame WHERE b IS NOT NULL"
)
res$collect()
```

    #> shape: (2, 2)
    #> ┌─────┬───────┐
    #> │ b   ┆ two_a │
    #> │ --- ┆ ---   │
    #> │ str ┆ i32   │
    #> ╞═════╪═══════╡
    #> │ x   ┆ 2     │
    #> │ z   ┆ 6     │
    #> └─────┴───────┘
