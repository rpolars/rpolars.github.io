

# Check if elements are NULL

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/after-wrappers.R#L20)

## Description

Returns a boolean Series indicating which values are null.

## Usage

<pre><code class='language-R'>Expr_is_null()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(list(x = c(1, NA, 3)))$select(pl$col("x")$is_null())
```

    #> shape: (3, 1)
    #> ┌───────┐
    #> │ x     │
    #> │ ---   │
    #> │ bool  │
    #> ╞═══════╡
    #> │ false │
    #> │ true  │
    #> │ false │
    #> └───────┘
