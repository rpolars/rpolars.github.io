

# Strip trailing characters

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/expr__string.R#L351)

## Description

Remove trailing characters.

## Usage

<pre><code class='language-R'>ExprStr_strip_chars_end(matches = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_strip_chars_end_:_matches">matches</code>
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
matched. <code>strip_chars_end()</code> removes characters at the end of
the string only. Use <code>strip_chars()</code> and
<code>strip_chars_start()</code> to remove characters from the left and
right or only from the left respectively.

## Value

Expr of String lowercase chars

## Examples

``` r
library(polars)

df = pl$DataFrame(foo = c(" hello", "\tworld"))
df$select(pl$col("foo")$str$strip_chars_end(" hel\trld"))
```

    #> shape: (2, 1)
    #> ┌────────┐
    #> │ foo    │
    #> │ ---    │
    #> │ str    │
    #> ╞════════╡
    #> │  hello │
    #> │    wo     │
    #> └────────┘

``` r
df$select(pl$col("foo")$str$strip_chars_end("rldhel\t "))
```

    #> shape: (2, 1)
    #> ┌────────┐
    #> │ foo    │
    #> │ ---    │
    #> │ str    │
    #> ╞════════╡
    #> │  hello │
    #> │    wo     │
    #> └────────┘
