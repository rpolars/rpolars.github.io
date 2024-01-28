

# Returns a column with a separate row for every string character

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/expr__string.R#L806)

## Description

Returns a column with a separate row for every string character

## Usage

<pre><code class='language-R'>ExprStr_explode()
</code></pre>

## Value

Expr: Series of dtype String.

## Examples

``` r
library(polars)

df = pl$DataFrame(a = c("foo", "bar"))
df$select(pl$col("a")$str$explode())
```

    #> shape: (6, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ str │
    #> ╞═════╡
    #> │ f   │
    #> │ o   │
    #> │ o   │
    #> │ b   │
    #> │ a   │
    #> │ r   │
    #> └─────┘
