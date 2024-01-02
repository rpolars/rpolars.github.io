
# Replace first matching regex/literal substring with a new string value

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/expr__string.R#L745)

## Description

Replace first matching regex/literal substring with a new string value

## Usage

<pre><code class='language-R'>ExprStr_replace(pattern, value, literal = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_replace_:_pattern">pattern</code>
</td>
<td>
Regex pattern, can be an Expr.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_replace_:_value">value</code>
</td>
<td>
Replacement, can be an Expr.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_replace_:_literal">literal</code>
</td>
<td>
Treat pattern as a literal string.
</td>
</tr>
</table>

## Value

Expr of Utf8 Series

## See Also

<code style="white-space: pre;">$str$replace_all()</code>: Replace all
matching regex/literal substrings.

## Examples

``` r
library(polars)

df = pl$DataFrame(id = c(1, 2), text = c("123abc", "abc456"))
df$with_columns(
  pl$col("text")$str$replace(r"{abc\b}", "ABC")
)
```

    #> shape: (2, 2)
    #> ┌─────┬────────┐
    #> │ id  ┆ text   │
    #> │ --- ┆ ---    │
    #> │ f64 ┆ str    │
    #> ╞═════╪════════╡
    #> │ 1.0 ┆ 123ABC │
    #> │ 2.0 ┆ abc456 │
    #> └─────┴────────┘
