

# Check if elements are not NULL

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/after-wrappers.R#L20)

## Description

Returns a boolean Series indicating which values are not null. Syntactic
sugar for <code style="white-space: pre;">$is_null()$not()</code>.

## Usage

<pre><code class='language-R'>Expr_is_not_null()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(list(x = c(1, NA, 3)))$select(pl$col("x")$is_not_null())
```

    #> shape: (3, 1)
    #> ┌───────┐
    #> │ x     │
    #> │ ---   │
    #> │ bool  │
    #> ╞═══════╡
    #> │ true  │
    #> │ false │
    #> │ true  │
    #> └───────┘
