

# Decode a value using the provided encoding

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__string.R#L555)

## Description

Decode a value using the provided encoding

## Usage

<pre><code class='language-R'>ExprStr_decode(encoding, ..., strict = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_decode_:_encoding">encoding</code>
</td>
<td>
Either ‘hex’ or ‘base64’.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_decode_:_...">…</code>
</td>
<td>
Not used currently.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_decode_:_strict">strict</code>
</td>
<td>
If <code>TRUE</code> (default), raise an error if the underlying value
cannot be decoded. Otherwise, replace it with a null value.
</td>
</tr>
</table>

## Value

String array with values decoded using provided encoding

## Examples

``` r
library(polars)

df = pl$DataFrame(strings = c("foo", "bar", NA))
df$select(pl$col("strings")$str$encode("hex"))
```

    #> shape: (3, 1)
    #> ┌─────────┐
    #> │ strings │
    #> │ ---     │
    #> │ str     │
    #> ╞═════════╡
    #> │ 666f6f  │
    #> │ 626172  │
    #> │ null    │
    #> └─────────┘

``` r
df$with_columns(
  pl$col("strings")$str$encode("base64")$alias("base64"), # notice DataType is not encoded
  pl$col("strings")$str$encode("hex")$alias("hex") # ... and must restored with cast
)$with_columns(
  pl$col("base64")$str$decode("base64")$alias("base64_decoded")$cast(pl$String),
  pl$col("hex")$str$decode("hex")$alias("hex_decoded")$cast(pl$String)
)
```

    #> shape: (3, 5)
    #> ┌─────────┬────────┬────────┬────────────────┬─────────────┐
    #> │ strings ┆ base64 ┆ hex    ┆ base64_decoded ┆ hex_decoded │
    #> │ ---     ┆ ---    ┆ ---    ┆ ---            ┆ ---         │
    #> │ str     ┆ str    ┆ str    ┆ str            ┆ str         │
    #> ╞═════════╪════════╪════════╪════════════════╪═════════════╡
    #> │ foo     ┆ Zm9v   ┆ 666f6f ┆ foo            ┆ foo         │
    #> │ bar     ┆ YmFy   ┆ 626172 ┆ bar            ┆ bar         │
    #> │ null    ┆ null   ┆ null   ┆ null           ┆ null        │
    #> └─────────┴────────┴────────┴────────────────┴─────────────┘
