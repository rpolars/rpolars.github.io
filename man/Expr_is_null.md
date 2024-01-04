
# Check if elements are NULL

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/#L)

## Description

Returns a boolean Series indicating which values are null.

## Usage

<pre><code class='language-R'>Expr_is_null
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
