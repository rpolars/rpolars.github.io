

# Returns string values in reversed order

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/expr__string.R#L839)

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
