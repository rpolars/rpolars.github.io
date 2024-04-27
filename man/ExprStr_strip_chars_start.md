

# Strip leading characters

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__string.R#L335)

## Description

Remove leading characters.

## Usage

<pre><code class='language-R'>ExprStr_strip_chars_start(matches = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="matches">matches</code>
</td>
<td>
The set of characters to be removed. All combinations of this set of
characters will be stripped. If <code>NULL</code> (default), all
whitespace is removed instead. This can be an Expr.
</td>
</tr>
</table>

## Details

This function will not strip any chars beyond the first char not
matched. <code>strip_chars_start()</code> removes characters at the
beginning of the string only. Use <code>strip_chars()</code> and
<code>strip_chars_end()</code> to remove characters from the left and
right or only from the right respectively.

## Value

Expr of String lowercase chars

## Examples

``` r
library(polars)

df = pl$DataFrame(foo = c(" hello", "\tworld"))
df$select(pl$col("foo")$str$strip_chars_start(" hel rld"))
```

    #> shape: (2, 1)
    #> ┌───────┐
    #> │ foo   │
    #> │ ---   │
    #> │ str   │
    #> ╞═══════╡
    #> │ o     │
    #> │    world │
    #> └───────┘
