

# Check if string contains a regex

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__string.R#L449)

## Description

Check if string contains a substring that matches a regex.

## Usage

<pre><code class='language-R'>ExprStr_contains(pattern, literal = FALSE, strict = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_contains_:_pattern">pattern</code>
</td>
<td>
String or Expr of a string, a valid regex pattern.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_contains_:_literal">literal</code>
</td>
<td>
Treat pattern as a literal string.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_contains_:_strict">strict</code>
</td>
<td>
Raise an error if the underlying pattern is not a valid regex
expression, otherwise replace the invalid regex with a null value.
</td>
</tr>
</table>

## Details

See also <code style="white-space: pre;">$str$starts_with()</code> and
<code style="white-space: pre;">$str$ends_with()</code>.

## Value

Expr returning a Boolean

## Examples

``` r
library(polars)

df = pl$DataFrame(a = c("Crab", "cat and dog", "rab$bit", NA))
df$select(
  pl$col("a"),
  pl$col("a")$str$contains("cat|bit")$alias("regex"),
  pl$col("a")$str$contains("rab$", literal = TRUE)$alias("literal")
)
```

    #> shape: (4, 3)
    #> ┌─────────────┬───────┬─────────┐
    #> │ a           ┆ regex ┆ literal │
    #> │ ---         ┆ ---   ┆ ---     │
    #> │ str         ┆ bool  ┆ bool    │
    #> ╞═════════════╪═══════╪═════════╡
    #> │ Crab        ┆ false ┆ false   │
    #> │ cat and dog ┆ true  ┆ false   │
    #> │ rab$bit     ┆ true  ┆ true    │
    #> │ null        ┆ null  ┆ null    │
    #> └─────────────┴───────┴─────────┘
