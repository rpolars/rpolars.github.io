

# Count elements

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/after-wrappers.R#L20)

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
