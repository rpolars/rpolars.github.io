

# Get the number of bytes in strings

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/expr__string.R#L213)

## Description

Get length of the strings as UInt32 (as number of bytes). Use
<code style="white-space: pre;">$str$len_chars()</code> to get the
number of characters.

## Usage

<pre><code class='language-R'>ExprStr_len_bytes()
</code></pre>

## Details

If you know that you are working with ASCII text, <code>lengths</code>
will be equivalent, and faster (returns length in terms of the number of
bytes).

## Value

Expr of u32

## Examples

``` r
library(polars)

pl$DataFrame(
  s = c("Café", NA, "345", "æøå")
)$select(
  pl$col("s"),
  pl$col("s")$str$len_bytes()$alias("lengths"),
  pl$col("s")$str$len_chars()$alias("n_chars")
)
```

    #> shape: (4, 3)
    #> ┌──────┬─────────┬─────────┐
    #> │ s    ┆ lengths ┆ n_chars │
    #> │ ---  ┆ ---     ┆ ---     │
    #> │ str  ┆ u32     ┆ u32     │
    #> ╞══════╪═════════╪═════════╡
    #> │ Café ┆ 5       ┆ 4       │
    #> │ null ┆ null    ┆ null    │
    #> │ 345  ┆ 3       ┆ 3       │
    #> │ æøå  ┆ 6       ┆ 3       │
    #> └──────┴─────────┴─────────┘
