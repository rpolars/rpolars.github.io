

# Convert a String column into an Int64 column with base radix

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__string.R#L887)

## Description

Convert a String column into an Int64 column with base radix

## Usage

<pre><code class='language-R'>ExprStr_to_integer(..., base = 10L, strict = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_to_integer_:_...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_to_integer_:_base">base</code>
</td>
<td>
A positive integer or expression which is the base of the string we are
parsing. Characters are parsed as column names. Default:
<code>10L</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_to_integer_:_strict">strict</code>
</td>
<td>
A logical. If <code>TRUE</code> (default), parsing errors or integer
overflow will raise an error. If <code>FALSE</code>, silently convert to
<code>null</code>.
</td>
</tr>
</table>

## Value

Expression of data type <code>Int64</code>.

## Examples

``` r
library(polars)

df = pl$DataFrame(bin = c("110", "101", "010", "invalid"))
df$with_columns(
  parsed = pl$col("bin")$str$to_integer(base = 2, strict = FALSE)
)
```

    #> shape: (4, 2)
    #> ┌─────────┬────────┐
    #> │ bin     ┆ parsed │
    #> │ ---     ┆ ---    │
    #> │ str     ┆ i64    │
    #> ╞═════════╪════════╡
    #> │ 110     ┆ 6      │
    #> │ 101     ┆ 5      │
    #> │ 010     ┆ 2      │
    #> │ invalid ┆ null   │
    #> └─────────┴────────┘

``` r
df = pl$DataFrame(hex = c("fa1e", "ff00", "cafe", NA))
df$with_columns(
  parsed = pl$col("hex")$str$to_integer(base = 16, strict = TRUE)
)
```

    #> shape: (4, 2)
    #> ┌──────┬────────┐
    #> │ hex  ┆ parsed │
    #> │ ---  ┆ ---    │
    #> │ str  ┆ i64    │
    #> ╞══════╪════════╡
    #> │ fa1e ┆ 64030  │
    #> │ ff00 ┆ 65280  │
    #> │ cafe ┆ 51966  │
    #> │ null ┆ null   │
    #> └──────┴────────┘
