

# Get the last value in a list

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__list.R#L216)

## Description

Get the last value in a list

## Usage

<pre><code class='language-R'>ExprList_last()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(a = list(3:1, NULL, 1:2)))
df$with_columns(
  last = pl$col("a")$list$last()
)
```

    #> shape: (3, 2)
    #> ┌───────────┬──────┐
    #> │ a         ┆ last │
    #> │ ---       ┆ ---  │
    #> │ list[i32] ┆ i32  │
    #> ╞═══════════╪══════╡
    #> │ [3, 2, 1] ┆ 1    │
    #> │ []        ┆ null │
    #> │ [1, 2]    ┆ 2    │
    #> └───────────┴──────┘
