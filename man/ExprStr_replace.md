

# Replace first matching regex/literal substring with a new string value

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__string.R#L794)

## Description

Replace first matching regex/literal substring with a new string value

## Usage

<pre><code class='language-R'>ExprStr_replace(pattern, value, ..., literal = FALSE, n = 1L)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pattern">pattern</code>
</td>
<td>
A character or something can be coerced to a string Expr of a valid
regex pattern, compatible with the
<a href="https://docs.rs/regex/latest/regex/">regex crate</a>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="value">value</code>
</td>
<td>
A character or an Expr of string that will replace the matched
substring.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="literal">literal</code>
</td>
<td>
Logical. If <code>TRUE</code> (default), treat <code>pattern</code> as a
literal string, not as a regular expression.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="n">n</code>
</td>
<td>
A number of matches to replace. Note that regex replacement with <code>n
\> 1</code> not yet supported, so raise an error if <code>n \> 1</code>
and <code>pattern</code> includes regex pattern and <code>literal =
FALSE</code>.
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

Expr of String type

## Capture groups

The dollar sign (<code>$</code>) is a special character related to
capture groups. To refer to a literal dollar sign, use
<code style="white-space: pre;">$$</code> instead or set
<code>literal</code> to <code>TRUE</code>.

## See Also

<ul>
<li>

<code>\<Expr\>$str$replace_all()</code>

</li>
</ul>

## Examples

``` r
library(polars)

df = pl$DataFrame(id = 1L:2L, text = c("123abc", "abc456"))
df$with_columns(pl$col("text")$str$replace(r"(abc\b)", "ABC"))
```

    #> shape: (2, 2)
    #> ┌─────┬────────┐
    #> │ id  ┆ text   │
    #> │ --- ┆ ---    │
    #> │ i32 ┆ str    │
    #> ╞═════╪════════╡
    #> │ 1   ┆ 123ABC │
    #> │ 2   ┆ abc456 │
    #> └─────┴────────┘

``` r
# Capture groups are supported.
# Use `${1}` in the value string to refer to the first capture group in the pattern,
# `${2}` to refer to the second capture group, and so on.
# You can also use named capture groups.
df = pl$DataFrame(word = c("hat", "hut"))
df$with_columns(
  positional = pl$col("word")$str$replace("h(.)t", "b${1}d"),
  named = pl$col("word")$str$replace("h(?<vowel>.)t", "b${vowel}d")
)
```

    #> shape: (2, 3)
    #> ┌──────┬────────────┬───────┐
    #> │ word ┆ positional ┆ named │
    #> │ ---  ┆ ---        ┆ ---   │
    #> │ str  ┆ str        ┆ str   │
    #> ╞══════╪════════════╪═══════╡
    #> │ hat  ┆ bad        ┆ bad   │
    #> │ hut  ┆ bud        ┆ bud   │
    #> └──────┴────────────┴───────┘

``` r
# Apply case-insensitive string replacement using the `(?i)` flag.
df = pl$DataFrame(
  city = "Philadelphia",
  season = c("Spring", "Summer", "Autumn", "Winter"),
  weather = c("Rainy", "Sunny", "Cloudy", "Snowy")
)
df$with_columns(
  pl$col("weather")$str$replace("(?i)foggy|rainy|cloudy|snowy", "Sunny")
)
```

    #> shape: (4, 3)
    #> ┌──────────────┬────────┬─────────┐
    #> │ city         ┆ season ┆ weather │
    #> │ ---          ┆ ---    ┆ ---     │
    #> │ str          ┆ str    ┆ str     │
    #> ╞══════════════╪════════╪═════════╡
    #> │ Philadelphia ┆ Spring ┆ Sunny   │
    #> │ Philadelphia ┆ Summer ┆ Sunny   │
    #> │ Philadelphia ┆ Autumn ┆ Sunny   │
    #> │ Philadelphia ┆ Winter ┆ Sunny   │
    #> └──────────────┴────────┴─────────┘
