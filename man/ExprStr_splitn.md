

# Split the string by a substring, restricted to returning at most <code>n</code> items

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__string.R#L753)

## Description

If the number of possible splits is less than <code>n-1</code>, the
remaining field elements will be null. If the number of possible splits
is <code>n-1</code> or greater, the last (nth) substring will contain
the remainder of the string.

## Usage

<pre><code class='language-R'>ExprStr_splitn(by, n)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_splitn_:_by">by</code>
</td>
<td>
Substring to split by.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_splitn_:_n">n</code>
</td>
<td>
Number of splits to make.
</td>
</tr>
</table>

## Value

Struct where each of <code>n</code> fields is of String type

## Examples

``` r
library(polars)

df = pl$DataFrame(s = c("a_1", NA, "c", "d_4_e"))
df$with_columns(
  s1 = pl$col("s")$str$splitn(by = "_", 1),
  s2 = pl$col("s")$str$splitn(by = "_", 2),
  s3 = pl$col("s")$str$splitn(by = "_", 3)
)
```

    #> shape: (4, 4)
    #> ┌───────┬───────────┬─────────────┬──────────────────┐
    #> │ s     ┆ s1        ┆ s2          ┆ s3               │
    #> │ ---   ┆ ---       ┆ ---         ┆ ---              │
    #> │ str   ┆ struct[1] ┆ struct[2]   ┆ struct[3]        │
    #> ╞═══════╪═══════════╪═════════════╪══════════════════╡
    #> │ a_1   ┆ {"a_1"}   ┆ {"a","1"}   ┆ {"a","1",null}   │
    #> │ null  ┆ {null}    ┆ {null,null} ┆ {null,null,null} │
    #> │ c     ┆ {"c"}     ┆ {"c",null}  ┆ {"c",null,null}  │
    #> │ d_4_e ┆ {"d_4_e"} ┆ {"d","4_e"} ┆ {"d","4","e"}    │
    #> └───────┴───────────┴─────────────┴──────────────────┘
