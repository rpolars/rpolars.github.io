

# Decode values using the provided encoding

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__binary.R#L92)

## Description

Decode values using the provided encoding

## Usage

<pre><code class='language-R'>ExprBin_decode(encoding, ..., strict = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="encoding">encoding</code>
</td>
<td>
A character, <code>“hex”</code> or <code>“base64”</code>. The encoding
to use.
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
<code id="strict">strict</code>
</td>
<td>
Raise an error if the underlying value cannot be decoded, otherwise mask
out with a <code>null</code> value.
</td>
</tr>
</table>

## Value

Expr of data type String.

## Examples

``` r
library(polars)

df = pl$DataFrame(
  name = c("black", "yellow", "blue"),
  code_hex = as_polars_series(c("000000", "ffff00", "0000ff"))$cast(pl$Binary),
  code_base64 = as_polars_series(c("AAAA", "//8A", "AAD/"))$cast(pl$Binary)
)

df$with_columns(
  decoded_hex = pl$col("code_hex")$bin$decode("hex"),
  decoded_base64 = pl$col("code_base64")$bin$decode("base64")
)
```

    #> shape: (3, 5)
    #> ┌────────┬───────────┬─────────────┬─────────────────┬─────────────────┐
    #> │ name   ┆ code_hex  ┆ code_base64 ┆ decoded_hex     ┆ decoded_base64  │
    #> │ ---    ┆ ---       ┆ ---         ┆ ---             ┆ ---             │
    #> │ str    ┆ binary    ┆ binary      ┆ binary          ┆ binary          │
    #> ╞════════╪═══════════╪═════════════╪═════════════════╪═════════════════╡
    #> │ black  ┆ b"000000" ┆ b"AAAA"     ┆ b"\x00\x00\x00" ┆ b"\x00\x00\x00" │
    #> │ yellow ┆ b"ffff00" ┆ b"//8A"     ┆ b"\xff\xff\x00" ┆ b"\xff\xff\x00" │
    #> │ blue   ┆ b"0000ff" ┆ b"AAD/"     ┆ b"\x00\x00\xff" ┆ b"\x00\x00\xff" │
    #> └────────┴───────────┴─────────────┴─────────────────┴─────────────────┘

``` r
# Set `strict = FALSE` to set invalid values to `null` instead of raising an error.
df = pl$DataFrame(
  colors = as_polars_series(c("000000", "ffff00", "invalid_value"))$cast(pl$Binary)
)
df$select(pl$col("colors")$bin$decode("hex", strict = FALSE))
```

    #> shape: (3, 1)
    #> ┌─────────────────┐
    #> │ colors          │
    #> │ ---             │
    #> │ binary          │
    #> ╞═════════════════╡
    #> │ b"\x00\x00\x00" │
    #> │ b"\xff\xff\x00" │
    #> │ null            │
    #> └─────────────────┘
