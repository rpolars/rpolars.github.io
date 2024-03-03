

# Vertically concatenate the string values in the column to a single string value.

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__string.R#L232)

## Description

Vertically concatenate the string values in the column to a single
string value.

## Usage

<pre><code class='language-R'>ExprStr_concat(delimiter = "", ..., ignore_nulls = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_concat_:_delimiter">delimiter</code>
</td>
<td>
The delimiter to insert between consecutive string values.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_concat_:_...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_concat_:_ignore_nulls">ignore_nulls</code>
</td>
<td>
Ignore null values (default). If <code>FALSE</code>, null values will be
propagated: if the column contains any null values, the output is null.
</td>
</tr>
</table>

## Value

Expr of String concatenated

## Examples

``` r
library(polars)

# concatenate a Series of strings to a single string
df = pl$DataFrame(foo = c(1, NA, 2))

df$select(pl$col("foo")$str$concat("-"))
```

    #> shape: (1, 1)
    #> ┌─────────┐
    #> │ foo     │
    #> │ ---     │
    #> │ str     │
    #> ╞═════════╡
    #> │ 1.0-2.0 │
    #> └─────────┘

``` r
df$select(pl$col("foo")$str$concat("-", ignore_nulls = FALSE))
```

    #> shape: (1, 1)
    #> ┌──────┐
    #> │ foo  │
    #> │ ---  │
    #> │ str  │
    #> ╞══════╡
    #> │ null │
    #> └──────┘
