
# Check if elements are not NULL

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/#L)

## Description

Returns a boolean Series indicating which values are not null. Syntactic
sugar for <code style="white-space: pre;">$is_null()$not()</code>.

## Usage

<pre><code class='language-R'>Expr_is_not_null
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
