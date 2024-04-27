

# Get the first value in a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__list.R#L202)

## Description

Get the first value in a list

## Usage

<pre><code class='language-R'>ExprList_first()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(a = list(3:1, NULL, 1:2)))
df$with_columns(
  first = pl$col("a")$list$first()
)
```

    #> shape: (3, 2)
    #> ┌───────────┬───────┐
    #> │ a         ┆ first │
    #> │ ---       ┆ ---   │
    #> │ list[i32] ┆ i32   │
    #> ╞═══════════╪═══════╡
    #> │ [3, 2, 1] ┆ 3     │
    #> │ []        ┆ null  │
    #> │ [1, 2]    ┆ 1     │
    #> └───────────┴───────┘
