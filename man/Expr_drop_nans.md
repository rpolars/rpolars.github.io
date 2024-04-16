

# Drop NaN

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/after-wrappers.R#L20)

## Description

Drop NaN

## Usage

<pre><code class='language-R'>Expr_drop_nans()
</code></pre>

## Details

Note that <code>NaN</code> values are not <code>null</code> values. Null
values correspond to NA in R.

## Value

Expr

## See Also

<code>drop_nulls()</code>

## Examples

``` r
library(polars)

pl$DataFrame(list(x = c(1, 2, NaN, NA)))$select(pl$col("x")$drop_nans())
```

    #> shape: (3, 1)
    #> ┌──────┐
    #> │ x    │
    #> │ ---  │
    #> │ f64  │
    #> ╞══════╡
    #> │ 1.0  │
    #> │ 2.0  │
    #> │ null │
    #> └──────┘
