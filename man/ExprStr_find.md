

# Return the index position of the first substring matching a pattern

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__string.R#L1024)

## Description

Return the index position of the first substring matching a pattern

## Usage

<pre><code class='language-R'>ExprStr_find(pattern, ..., literal = FALSE, strict = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_find_:_pattern">pattern</code>
</td>
<td>
A character or something can be coerced to a string Expr of a valid
regex pattern, compatible with the
<a href="https://docs.rs/regex/latest/regex/">regex crate</a>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_find_:_...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_find_:_literal">literal</code>
</td>
<td>
Logical. If <code>TRUE</code> (default), treat <code>pattern</code> as a
literal string, not as a regular expression.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_find_:_strict">strict</code>
</td>
<td>
Logical. If <code>TRUE</code> (default), raise an error if the
underlying pattern is not a valid regex, otherwise mask out with a null
value.
</td>
</tr>
</table>

## Details

To modify regular expression behaviour (such as case-sensitivity) with
flags, use the inline <code>(?iLmsuxU)</code> syntax. See the regex
crate’s section on
<a href="https://docs.rs/regex/latest/regex/#grouping-and-flags">grouping
and flags</a> for additional information about the use of inline
expression modifiers.

## Value

An Expr of data type UInt32

## See Also

<ul>
<li>

<code>$str$start_with()</code>: Check if string values start with a
substring.

</li>
<li>

<code>$str$ends_with()</code>: Check if string values end with a
substring.

</li>
<li>

<code>$str$contains()</code>: Check if string contains a substring that
matches a pattern.

</li>
</ul>

## Examples

``` r
library(polars)

pl$DataFrame(s = c("AAA", "aAa", "aaa"))$with_columns(
  default_match = pl$col("s")$str$find("Aa"),
  insensitive_match = pl$col("s")$str$find("(?i)Aa")
)
```

    #> shape: (3, 3)
    #> ┌─────┬───────────────┬───────────────────┐
    #> │ s   ┆ default_match ┆ insensitive_match │
    #> │ --- ┆ ---           ┆ ---               │
    #> │ str ┆ u32           ┆ u32               │
    #> ╞═════╪═══════════════╪═══════════════════╡
    #> │ AAA ┆ null          ┆ 0                 │
    #> │ aAa ┆ 1             ┆ 0                 │
    #> │ aaa ┆ null          ┆ 0                 │
    #> └─────┴───────────────┴───────────────────┘
