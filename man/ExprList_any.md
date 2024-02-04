

# Evaluate whether any boolean values in a list are true

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/expr__list.R#L472)

## Description

Evaluate whether any boolean values in a list are true

## Usage

<pre><code class='language-R'>ExprList_any()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  list(a = list(c(TRUE, TRUE), c(FALSE, TRUE), c(FALSE, FALSE), NA, c()))
)
df$with_columns(any = pl$col("a")$list$any())
```

    #> shape: (5, 2)
    #> ┌────────────────┬───────┐
    #> │ a              ┆ any   │
    #> │ ---            ┆ ---   │
    #> │ list[bool]     ┆ bool  │
    #> ╞════════════════╪═══════╡
    #> │ [true, true]   ┆ true  │
    #> │ [false, true]  ┆ true  │
    #> │ [false, false] ┆ false │
    #> │ [null]         ┆ false │
    #> │ []             ┆ false │
    #> └────────────────┴───────┘
