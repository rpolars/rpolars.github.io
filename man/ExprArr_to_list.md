

# Convert an Array column into a List column with the same inner data type

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__array.R#L291)

## Description

Convert an Array column into a List column with the same inner data type

## Usage

<pre><code class='language-R'>ExprArr_to_list()
</code></pre>

## Value

Expr of data type List

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = list(c(1, 2), c(3, 4)),
  schema = list(a = pl$Array(pl$Int8, 2))
)

df$with_columns(
  list = pl$col("a")$arr$to_list()
)
```

    #> shape: (2, 2)
    #> ┌──────────────┬──────────┐
    #> │ a            ┆ list     │
    #> │ ---          ┆ ---      │
    #> │ array[i8, 2] ┆ list[i8] │
    #> ╞══════════════╪══════════╡
    #> │ [1, 2]       ┆ [1, 2]   │
    #> │ [3, 4]       ┆ [3, 4]   │
    #> └──────────────┴──────────┘
