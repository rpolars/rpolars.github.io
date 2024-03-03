

# Check if string ends with a regex

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__string.R#L458)

## Description

Check if string values end with a substring.

## Usage

<pre><code class='language-R'>ExprStr_ends_with(sub)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_ends_with_:_sub">sub</code>
</td>
<td>
Suffix substring or Expr.
</td>
</tr>
</table>

## Details

See also <code style="white-space: pre;">$str$starts_with()</code> and
<code style="white-space: pre;">$str$contains()</code>.

## Value

Expr returning a Boolean

## Examples

``` r
library(polars)

df = pl$DataFrame(fruits = c("apple", "mango", NA))
df$select(
  pl$col("fruits"),
  pl$col("fruits")$str$ends_with("go")$alias("has_suffix")
)
```

    #> shape: (3, 2)
    #> ┌────────┬────────────┐
    #> │ fruits ┆ has_suffix │
    #> │ ---    ┆ ---        │
    #> │ str    ┆ bool       │
    #> ╞════════╪════════════╡
    #> │ apple  ┆ false      │
    #> │ mango  ┆ true       │
    #> │ null   ┆ null       │
    #> └────────┴────────────┘
