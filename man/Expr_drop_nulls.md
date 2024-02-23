

# Drop missing values

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/after-wrappers.R#L20)

## Description

Drop missing values

## Usage

<pre><code class='language-R'>Expr_drop_nulls()
</code></pre>

## Value

Expr

## See Also

<code>drop_nans()</code>

## Examples

``` r
library(polars)

pl$DataFrame(list(x = c(1, 2, NaN, NA)))$select(pl$col("x")$drop_nulls())
```

    #> shape: (3, 1)
    #> ┌─────┐
    #> │ x   │
    #> │ --- │
    #> │ f64 │
    #> ╞═════╡
    #> │ 1.0 │
    #> │ 2.0 │
    #> │ NaN │
    #> └─────┘
