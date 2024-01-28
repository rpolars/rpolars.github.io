

# Extract all matches for the given regex pattern

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/expr__string.R#L627)

## Description

Extracts all matches for the given regex pattern. Extracts each
successive non-overlapping regex match in an individual string as an
array.

## Usage

<pre><code class='language-R'>ExprStr_extract_all(pattern)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_extract_all_:_pattern">pattern</code>
</td>
<td>
A valid regex pattern
</td>
</tr>
</table>

## Value

<code>List\[String\]</code> array. Contain null if original value is
null or regex capture nothing.

## Examples

``` r
library(polars)

df = pl$DataFrame(foo = c("123 bla 45 asd", "xyz 678 910t"))
df$select(
  pl$col("foo")$str$extract_all(r"((\d+))")$alias("extracted_nrs")
)
```

    #> shape: (2, 1)
    #> ┌────────────────┐
    #> │ extracted_nrs  │
    #> │ ---            │
    #> │ list[str]      │
    #> ╞════════════════╡
    #> │ ["123", "45"]  │
    #> │ ["678", "910"] │
    #> └────────────────┘
