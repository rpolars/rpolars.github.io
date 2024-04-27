

# Evaluate whether all boolean values in an array are true

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__array.R#L240)

## Description

Evaluate whether all boolean values in an array are true

## Usage

<pre><code class='language-R'>ExprArr_all()
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
df$with_columns(all = pl$col("values")$arr$all())
```

    #> shape: (4, 2)
    #> ┌────────────────┬───────┐
    #> │ values         ┆ all   │
    #> │ ---            ┆ ---   │
    #> │ array[bool, 2] ┆ bool  │
    #> ╞════════════════╪═══════╡
    #> │ [true, true]   ┆ true  │
    #> │ [false, true]  ┆ false │
    #> │ [false, false] ┆ false │
    #> │ [null, null]   ┆ true  │
    #> └────────────────┴───────┘
