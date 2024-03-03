

# Strip leading and trailing characters

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__string.R#L301)

## Description

Remove leading and trailing characters.

## Usage

<pre><code class='language-R'>ExprStr_strip_chars(matches = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_strip_chars_:_matches">matches</code>
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
matched. <code>strip_chars()</code> removes characters at the beginning
and the end of the string. Use <code>strip_chars_start()</code> and
<code>strip_chars_end()</code> to remove characters only from left and
right respectively.

## Value

Expr of String lowercase chars

## Examples

``` r
library(polars)

df = pl$DataFrame(foo = c(" hello", "\tworld"))
df$select(pl$col("foo")$str$strip_chars())
```

    #> shape: (2, 1)
    #> ┌───────┐
    #> │ foo   │
    #> │ ---   │
    #> │ str   │
    #> ╞═══════╡
    #> │ hello │
    #> │ world │
    #> └───────┘

``` r
df$select(pl$col("foo")$str$strip_chars(" hel rld"))
```

    #> shape: (2, 1)
    #> ┌─────┐
    #> │ foo │
    #> │ --- │
    #> │ str │
    #> ╞═════╡
    #> │ o   │
    #> │    wo  │
    #> └─────┘
