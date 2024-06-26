

# Use the aho-corasick algorithm to find matches

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__string.R#L927)

## Description

This function determines if any of the patterns find a match.

## Usage

<pre><code class='language-R'>ExprStr_contains_any(patterns, ..., ascii_case_insensitive = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="patterns">patterns</code>
</td>
<td>
Character vector or something can be coerced to strings Expr of a valid
regex pattern, compatible with the
<a href="https://docs.rs/regex/latest/regex/">regex crate</a>.
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
<code id="ascii_case_insensitive">ascii_case_insensitive</code>
</td>
<td>
Enable ASCII-aware case insensitive matching. When this option is
enabled, searching will be performed without respect to case for ASCII
letters (a-z and A-Z) only.
</td>
</tr>
</table>

## Value

Expr of Boolean data type

## See Also

<ul>
<li>

<code>\<Expr\>$str$contains()</code>

</li>
</ul>

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

df$with_columns(
  contains_any = pl$col("lyrics")$str$contains_any(c("you", "me"))
)
```

    #> shape: (3, 2)
    #> ┌───────────────────────────────────┬──────────────┐
    #> │ lyrics                            ┆ contains_any │
    #> │ ---                               ┆ ---          │
    #> │ str                               ┆ bool         │
    #> ╞═══════════════════════════════════╪══════════════╡
    #> │ Everybody wants to rule the worl… ┆ false        │
    #> │ Tell me what you want, what you … ┆ true         │
    #> │ Can you feel the love tonight     ┆ true         │
    #> └───────────────────────────────────┴──────────────┘
