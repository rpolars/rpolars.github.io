

# Extract the target capture group from provided patterns

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__string.R#L637)

## Description

Extract the target capture group from provided patterns

## Usage

<pre><code class='language-R'>ExprStr_extract(pattern, group_index)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pattern">pattern</code>
</td>
<td>
A valid regex pattern. Can be an Expr or something coercible to an Expr.
Strings are parsed as column names.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="group_index">group_index</code>
</td>
<td>
Index of the targeted capture group. Group 0 means the whole pattern,
first group begin at index 1 (default).
</td>
</tr>
</table>

## Value

String array. Contains null if original value is null or regex capture
nothing.

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = c(
    "http://vote.com/ballon_dor?candidate=messi&ref=polars",
    "http://vote.com/ballon_dor?candidat=jorginho&ref=polars",
    "http://vote.com/ballon_dor?candidate=ronaldo&ref=polars"
  )
)
df$with_columns(
  extracted = pl$col("a")$str$extract(pl$lit(r"(candidate=(\w+))"), 1)
)
```

    #> shape: (3, 2)
    #> ┌───────────────────────────────────┬───────────┐
    #> │ a                                 ┆ extracted │
    #> │ ---                               ┆ ---       │
    #> │ str                               ┆ str       │
    #> ╞═══════════════════════════════════╪═══════════╡
    #> │ http://vote.com/ballon_dor?candi… ┆ messi     │
    #> │ http://vote.com/ballon_dor?candi… ┆ null      │
    #> │ http://vote.com/ballon_dor?candi… ┆ ronaldo   │
    #> └───────────────────────────────────┴───────────┘
