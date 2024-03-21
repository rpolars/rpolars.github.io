

# Split the string by a substring using <code>n</code> splits

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__string.R#L714)

## Description

This results in a struct of <code>n+1</code> fields. If it cannot make
<code>n</code> splits, the remaining field elements will be null.

## Usage

<pre><code class='language-R'>ExprStr_split_exact(by, n, inclusive = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_split_exact_:_by">by</code>
</td>
<td>
Substring to split by.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_split_exact_:_n">n</code>
</td>
<td>
Number of splits to make.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_split_exact_:_inclusive">inclusive</code>
</td>
<td>
If <code>TRUE</code>, include the split character/string in the results.
</td>
</tr>
</table>

## Value

Struct where each of n+1 fields is of String type

## Examples

``` r
library(polars)

df = pl$DataFrame(s = c("a_1", NA, "c", "d_4"))
df$with_columns(
  split = pl$col("s")$str$split_exact(by = "_", 1),
  split_inclusive = pl$col("s")$str$split_exact(by = "_", 1, inclusive = TRUE)
)
```

    #> shape: (4, 3)
    #> ┌──────┬─────────────┬─────────────────┐
    #> │ s    ┆ split       ┆ split_inclusive │
    #> │ ---  ┆ ---         ┆ ---             │
    #> │ str  ┆ struct[2]   ┆ struct[2]       │
    #> ╞══════╪═════════════╪═════════════════╡
    #> │ a_1  ┆ {"a","1"}   ┆ {"a_","1"}      │
    #> │ null ┆ {null,null} ┆ {null,null}     │
    #> │ c    ┆ {"c",null}  ┆ {"c",null}      │
    #> │ d_4  ┆ {"d","4"}   ┆ {"d_","4"}      │
    #> └──────┴─────────────┴─────────────────┘
