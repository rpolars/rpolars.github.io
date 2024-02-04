

# decode

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/expr__binary.R#L70)

## Description

Decode a value using the provided encoding.

## Usage

<pre><code class='language-R'>ExprBin_decode(encoding, strict = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprBin_decode_:_encoding">encoding</code>
</td>
<td>
binary choice either ‘hex’ or ‘base64’
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprBin_decode_:_strict">strict</code>
</td>
<td>
Raise an error if the underlying value cannot be decoded, otherwise mask
out with a null value.
</td>
</tr>
</table>

## Value

binary array with values decoded using provided encoding
