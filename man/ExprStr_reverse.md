

# Returns string values in reversed order

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/expr__string.R#L841)

## Description

Returns string values in reversed order

## Usage

<pre><code class='language-R'>ExprStr_reverse()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(text = c("foo", "bar", NA))
df$with_columns(reversed = pl$col("text")$str$reverse())
```

    #> shape: (3, 2)
    #> ┌──────┬──────────┐
    #> │ text ┆ reversed │
    #> │ ---  ┆ ---      │
    #> │ str  ┆ str      │
    #> ╞══════╪══════════╡
    #> │ foo  ┆ oof      │
    #> │ bar  ┆ rab      │
    #> │ null ┆ null     │
    #> └──────┴──────────┘
