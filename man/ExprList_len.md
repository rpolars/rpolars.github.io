

# Get the length of each list

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__list.R#L11)

## Description

Return the number of elements in each list. Null values are counted in
the total.

## Usage

<pre><code class='language-R'>ExprList_len()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(list_of_strs = list(c("a", "b", NA), "c")))
df$with_columns(len_list = pl$col("list_of_strs")$list$len())
```

    #> shape: (2, 2)
    #> ┌──────────────────┬──────────┐
    #> │ list_of_strs     ┆ len_list │
    #> │ ---              ┆ ---      │
    #> │ list[str]        ┆ u32      │
    #> ╞══════════════════╪══════════╡
    #> │ ["a", "b", null] ┆ 3        │
    #> │ ["c"]            ┆ 1        │
    #> └──────────────────┴──────────┘
