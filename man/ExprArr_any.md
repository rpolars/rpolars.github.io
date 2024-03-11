

# Evaluate whether any boolean values in an array are true

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/expr__array.R#L258)

## Description

Evaluate whether any boolean values in an array are true

## Usage

<pre><code class='language-R'>ExprArr_any()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  values = list(c(TRUE, TRUE), c(FALSE, TRUE), c(FALSE, FALSE), c(NA, NA)),
  schema = list(values = pl$Array(pl$Boolean, 2))
)
df$with_columns(any = pl$col("values")$arr$any())
```

    #> shape: (4, 2)
    #> ┌────────────────┬───────┐
    #> │ values         ┆ any   │
    #> │ ---            ┆ ---   │
    #> │ array[bool, 2] ┆ bool  │
    #> ╞════════════════╪═══════╡
    #> │ [true, true]   ┆ true  │
    #> │ [false, true]  ┆ true  │
    #> │ [false, false] ┆ false │
    #> │ [null, null]   ┆ false │
    #> └────────────────┴───────┘
