
# Returns string values in reversed order

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/expr__string.R#L833)

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
