

# Get the length of each list

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/expr__list.R#L11)

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
