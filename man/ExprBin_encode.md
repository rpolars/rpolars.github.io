

# Encode a value using the provided encoding

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/expr__binary.R#L56)

## Description

Encode a value using the provided encoding

## Usage

<pre><code class='language-R'>ExprBin_encode(encoding)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprBin_encode_:_encoding">encoding</code>
</td>
<td>
A character, <code>“hex”</code> or <code>“base64”</code>. The encoding
to use.
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
  code = as_polars_series(
    c("000000", "ffff00", "0000ff")
  )$cast(pl$Binary)$bin$decode("hex")
)

df$with_columns(encoded = pl$col("code")$bin$encode("hex"))
```

    #> shape: (3, 3)
    #> ┌────────┬─────────────────┬─────────┐
    #> │ name   ┆ code            ┆ encoded │
    #> │ ---    ┆ ---             ┆ ---     │
    #> │ str    ┆ binary          ┆ str     │
    #> ╞════════╪═════════════════╪═════════╡
    #> │ black  ┆ b"\x00\x00\x00" ┆ 000000  │
    #> │ yellow ┆ b"\xff\xff\x00" ┆ ffff00  │
    #> │ blue   ┆ b"\x00\x00\xff" ┆ 0000ff  │
    #> └────────┴─────────────────┴─────────┘
