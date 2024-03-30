

# Replace all matching regex/literal substrings with a new string value

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__string.R#L797)

## Description

Replace all matching regex/literal substrings with a new string value

## Usage

<pre><code class='language-R'>ExprStr_replace_all(pattern, value, literal = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_replace_all_:_pattern">pattern</code>
</td>
<td>
Regex pattern, can be an Expr.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_replace_all_:_value">value</code>
</td>
<td>
Replacement, can be an Expr.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_replace_all_:_literal">literal</code>
</td>
<td>
Treat pattern as a literal string.
</td>
</tr>
</table>

## Value

Expr of String Series

## See Also

<code style="white-space: pre;">$str$replace()</code>: Replace first
matching regex/literal substring.

## Examples

``` r
library(polars)

df = pl$DataFrame(id = c(1, 2), text = c("abcabc", "123a123"))
df$with_columns(
  pl$col("text")$str$replace_all("a", "-")
)
```

    #> shape: (2, 2)
    #> ┌─────┬─────────┐
    #> │ id  ┆ text    │
    #> │ --- ┆ ---     │
    #> │ f64 ┆ str     │
    #> ╞═════╪═════════╡
    #> │ 1.0 ┆ -bc-bc  │
    #> │ 2.0 ┆ 123-123 │
    #> └─────┴─────────┘
