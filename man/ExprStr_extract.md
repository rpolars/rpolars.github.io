
# Extract the target capture group from provided patterns

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__string.R#L607)

## Description

Extract the target capture group from provided patterns

## Usage

<pre><code class='language-R'>ExprStr_extract(pattern, group_index)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_extract_:_pattern">pattern</code>
</td>
<td>
A valid regex pattern
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_extract_:_group_index">group_index</code>
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
df$select(
  pl$col("a")$str$extract(r"(candidate=(\w+))", 1)
)
```

    #> shape: (3, 1)
    #> ┌─────────┐
    #> │ a       │
    #> │ ---     │
    #> │ str     │
    #> ╞═════════╡
    #> │ messi   │
    #> │ null    │
    #> │ ronaldo │
    #> └─────────┘
