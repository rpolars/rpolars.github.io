

# Extract all capture groups for the given regex pattern

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__string.R#L1003)

## Description

Extract all capture groups for the given regex pattern

## Usage

<pre><code class='language-R'>ExprStr_extract_groups(pattern)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_extract_groups_:_pattern">pattern</code>
</td>
<td>
A character of a valid regular expression pattern containing at least
one capture group, compatible with the
<a href="https://docs.rs/regex/latest/regex/">regex crate</a>.
</td>
</tr>
</table>

## Details

All group names are strings. If your pattern contains unnamed groups,
their numerical position is converted to a string. See examples.

## Value

Expr of data type Struct with fields of data type <code>String</code>.

## Examples

``` r
library(polars)

df = pl$DataFrame(
  url = c(
    "http://vote.com/ballon_dor?candidate=messi&ref=python",
    "http://vote.com/ballon_dor?candidate=weghorst&ref=polars",
    "http://vote.com/ballon_dor?error=404&ref=rust"
  )
)

pattern = r"(candidate=(?<candidate>\w+)&ref=(?<ref>\w+))"

df$with_columns(
  captures = pl$col("url")$str$extract_groups(pattern)
)$unnest("captures")
```

    #> shape: (3, 3)
    #> ┌───────────────────────────────────┬───────────┬────────┐
    #> │ url                               ┆ candidate ┆ ref    │
    #> │ ---                               ┆ ---       ┆ ---    │
    #> │ str                               ┆ str       ┆ str    │
    #> ╞═══════════════════════════════════╪═══════════╪════════╡
    #> │ http://vote.com/ballon_dor?candi… ┆ messi     ┆ python │
    #> │ http://vote.com/ballon_dor?candi… ┆ weghorst  ┆ polars │
    #> │ http://vote.com/ballon_dor?error… ┆ null      ┆ null   │
    #> └───────────────────────────────────┴───────────┴────────┘

``` r
# If the groups are unnamed, their numerical position (as a string) is used:

pattern = r"(candidate=(\w+)&ref=(\w+))"

df$with_columns(
  captures = pl$col("url")$str$extract_groups(pattern)
)$unnest("captures")
```

    #> shape: (3, 3)
    #> ┌───────────────────────────────────┬──────────┬────────┐
    #> │ url                               ┆ 1        ┆ 2      │
    #> │ ---                               ┆ ---      ┆ ---    │
    #> │ str                               ┆ str      ┆ str    │
    #> ╞═══════════════════════════════════╪══════════╪════════╡
    #> │ http://vote.com/ballon_dor?candi… ┆ messi    ┆ python │
    #> │ http://vote.com/ballon_dor?candi… ┆ weghorst ┆ polars │
    #> │ http://vote.com/ballon_dor?error… ┆ null     ┆ null   │
    #> └───────────────────────────────────┴──────────┴────────┘
