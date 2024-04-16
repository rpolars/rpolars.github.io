

# Count all successive non-overlapping regex matches

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/expr__string.R#L675)

## Description

Count all successive non-overlapping regex matches

## Usage

<pre><code class='language-R'>ExprStr_count_matches(pattern, ..., literal = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_count_matches_:_pattern">pattern</code>
</td>
<td>
A character or something can be coerced to a string Expr of a valid
regex pattern, compatible with the
<a href="https://docs.rs/regex/latest/regex/">regex crate</a>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_count_matches_:_...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_count_matches_:_literal">literal</code>
</td>
<td>
Logical. If <code>TRUE</code> (default), treat <code>pattern</code> as a
literal string, not as a regular expression.
</td>
</tr>
</table>

## Value

Expr of data type <code>UInt32</code>. Returns <code>null</code> if the
original value is <code>null</code>.

## Examples

``` r
library(polars)

df = pl$DataFrame(foo = c("12 dbc 3xy", "cat\\w", "1zy3\\d\\d", NA))

df$with_columns(
  count_digits = pl$col("foo")$str$count_matches(r"(\d)"),
  count_slash_d = pl$col("foo")$str$count_matches(r"(\d)", literal = TRUE)
)
```

    #> shape: (4, 3)
    #> ┌────────────┬──────────────┬───────────────┐
    #> │ foo        ┆ count_digits ┆ count_slash_d │
    #> │ ---        ┆ ---          ┆ ---           │
    #> │ str        ┆ u32          ┆ u32           │
    #> ╞════════════╪══════════════╪═══════════════╡
    #> │ 12 dbc 3xy ┆ 3            ┆ 0             │
    #> │ cat\w      ┆ 0            ┆ 0             │
    #> │ 1zy3\d\d   ┆ 2            ┆ 2             │
    #> │ null       ┆ null         ┆ null          │
    #> └────────────┴──────────────┴───────────────┘
