

# Count unique values

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/after-wrappers.R#L20)

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
