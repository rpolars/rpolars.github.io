

# Evaluate whether any boolean values in an array are true

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/expr__array.R#L214)

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
