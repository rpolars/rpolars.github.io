

# Drop NaN

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/after-wrappers.R#L20)

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
