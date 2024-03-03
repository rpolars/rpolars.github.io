

# Evaluate whether all boolean values in a list are true

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__list.R#L499)

## Description

Evaluate whether all boolean values in a list are true

## Usage

<pre><code class='language-R'>ExprList_all()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  list(a = list(c(TRUE, TRUE), c(FALSE, TRUE), c(FALSE, FALSE), NA, c()))
)
df$with_columns(all = pl$col("a")$list$all())
```

    #> shape: (5, 2)
    #> ┌────────────────┬───────┐
    #> │ a              ┆ all   │
    #> │ ---            ┆ ---   │
    #> │ list[bool]     ┆ bool  │
    #> ╞════════════════╪═══════╡
    #> │ [true, true]   ┆ true  │
    #> │ [false, true]  ┆ false │
    #> │ [false, false] ┆ false │
    #> │ [null]         ┆ true  │
    #> │ []             ┆ true  │
    #> └────────────────┴───────┘
