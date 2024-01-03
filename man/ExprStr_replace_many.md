
# Use the aho-corasick algorithm to replace many matches

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__string.R#L898)

## Description

This function replaces several matches at once.

## Usage

<pre><code class='language-R'>ExprStr_replace_many(patterns, replace_with, ascii_case_insensitive = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_replace_many_:_patterns">patterns</code>
</td>
<td>
String patterns to search. Can be an Expr.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_replace_many_:_replace_with">replace_with</code>
</td>
<td>
A vector of strings used as replacements. If this is of length 1, then
it is applied to all matches. Otherwise, it must be of same length as
the <code>patterns</code> argument.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_replace_many_:_ascii_case_insensitive">ascii_case_insensitive</code>
</td>
<td>
Enable ASCII-aware case insensitive matching. When this option is
enabled, searching will be performed without respect to case for ASCII
letters (a-z and A-Z) only.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  lyrics = c(
    "Everybody wants to rule the world",
    "Tell me what you want, what you really really want",
    "Can you feel the love tonight"
  )
)

# a replacement of length 1 is applied to all matches
df$with_columns(
  remove_pronouns = pl$col("lyrics")$str$replace_many(c("you", "me"), "")
)
```

    #> shape: (3, 2)
    #> ┌───────────────────────────────────┬───────────────────────────────────┐
    #> │ lyrics                            ┆ remove_pronouns                   │
    #> │ ---                               ┆ ---                               │
    #> │ str                               ┆ str                               │
    #> ╞═══════════════════════════════════╪═══════════════════════════════════╡
    #> │ Everybody wants to rule the worl… ┆ Everybody wants to rule the worl… │
    #> │ Tell me what you want, what you … ┆ Tell  what  want, what  really r… │
    #> │ Can you feel the love tonight     ┆ Can  feel the love tonight        │
    #> └───────────────────────────────────┴───────────────────────────────────┘

``` r
# if there are more than one replacement, the patterns and replacements are
# matched
df$with_columns(
  fake_pronouns = pl$col("lyrics")$str$replace_many(c("you", "me"), c("foo", "bar"))
)
```

    #> shape: (3, 2)
    #> ┌───────────────────────────────────┬───────────────────────────────────┐
    #> │ lyrics                            ┆ fake_pronouns                     │
    #> │ ---                               ┆ ---                               │
    #> │ str                               ┆ str                               │
    #> ╞═══════════════════════════════════╪═══════════════════════════════════╡
    #> │ Everybody wants to rule the worl… ┆ Everybody wants to rule the worl… │
    #> │ Tell me what you want, what you … ┆ Tell bar what foo want, what foo… │
    #> │ Can you feel the love tonight     ┆ Can foo feel the love tonight     │
    #> └───────────────────────────────────┴───────────────────────────────────┘
