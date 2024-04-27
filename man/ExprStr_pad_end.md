

# Left justify strings

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__string.R#L410)

## Description

Return the string left justified in a string of length
<code>width</code>.

## Usage

<pre><code class='language-R'>ExprStr_pad_end(width, fillchar = " ")
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="width">width</code>
</td>
<td>
Justify left to this length.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="fillchar">fillchar</code>
</td>
<td>
Fill with this ASCII character.
</td>
</tr>
</table>

## Details

Padding is done using the specified <code>fillchar</code>. The original
string is returned if <code>width</code> is less than or equal to
<code>len(s)</code>.

## Value

Expr of String

## Examples

``` r
library(polars)

df = pl$DataFrame(a = c("cow", "monkey", NA, "hippopotamus"))
df$select(pl$col("a")$str$pad_end(8, "*"))
```

    #> shape: (4, 1)
    #> ┌──────────────┐
    #> │ a            │
    #> │ ---          │
    #> │ str          │
    #> ╞══════════════╡
    #> │ cow*****     │
    #> │ monkey**     │
    #> │ null         │
    #> │ hippopotamus │
    #> └──────────────┘
