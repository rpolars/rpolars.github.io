

# Count unique values

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/after-wrappers.R#L20)

## Description

Return a count of the unique values in the order of appearance. This
method differs from
<code style="white-space: pre;">$value_counts()</code> in that it does
not return the values, only the counts and it might be faster.

## Usage

<pre><code class='language-R'>Expr_unique_counts()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(iris)$select(pl$col("Species")$unique_counts())
```

    #> shape: (3, 1)
    #> ┌─────────┐
    #> │ Species │
    #> │ ---     │
    #> │ u32     │
    #> ╞═════════╡
    #> │ 50      │
    #> │ 50      │
    #> │ 50      │
    #> └─────────┘
