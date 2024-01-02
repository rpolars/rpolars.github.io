
# Arg max sublists

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/expr__list.R#L270)

## Description

Retrieve the index of the maximum value in every sublist.

## Usage

<pre><code class='language-R'>ExprList_arg_max()
</code></pre>

## Format

function

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(list(s = list(1:2, 2:1)))
df$select(pl$col("s")$list$arg_max())
```

    #> shape: (2, 1)
    #> ┌─────┐
    #> │ s   │
    #> │ --- │
    #> │ u32 │
    #> ╞═════╡
    #> │ 1   │
    #> │ 0   │
    #> └─────┘
