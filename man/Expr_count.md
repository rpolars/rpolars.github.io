

# Count elements

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/after-wrappers.R#L20)

## Description

Count the number of elements in this expression. Note that
<code>NULL</code> values are also counted.
<code style="white-space: pre;">$len()</code> is an alias.

## Usage

<pre><code class='language-R'>Expr_count()

Expr_len()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(
  all = c(TRUE, TRUE),
  any = c(TRUE, FALSE),
  none = c(FALSE, FALSE)
)$select(
  pl$all()$count()
)
```

    #> shape: (1, 3)
    #> ┌─────┬─────┬──────┐
    #> │ all ┆ any ┆ none │
    #> │ --- ┆ --- ┆ ---  │
    #> │ u32 ┆ u32 ┆ u32  │
    #> ╞═════╪═════╪══════╡
    #> │ 2   ┆ 2   ┆ 2    │
    #> └─────┴─────┴──────┘
