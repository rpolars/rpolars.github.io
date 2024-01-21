
# Get the length of each list

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__list.R#L11)

## Description

Return the number of elements in each list. Null values are counted in
the total. <code style="white-space: pre;">$list$lengths()</code> is
deprecated.

## Usage

<pre><code class='language-R'>ExprList_len()

ExprList_lengths()
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
