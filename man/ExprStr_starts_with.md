

# Check if string starts with a regex

[**Source code**](https://github.com/pola-rs/r-polars/tree/8387e0a88c6889e6449b053999aada405c241066/R/expr__string.R#L478)

## Description

Check if string values starts with a substring.

## Usage

<pre><code class='language-R'>ExprStr_starts_with(sub)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_starts_with_:_sub">sub</code>
</td>
<td>
Prefix substring or Expr.
</td>
</tr>
</table>

## Details

See also <code style="white-space: pre;">$str$contains()</code> and
<code style="white-space: pre;">$str$ends_with()</code>.

## Value

Expr returning a Boolean

## Examples

``` r
library(polars)

df = pl$DataFrame(fruits = c("apple", "mango", NA))
df$select(
  pl$col("fruits"),
  pl$col("fruits")$str$starts_with("app")$alias("has_suffix")
)
```

    #> shape: (3, 2)
    #> ┌────────┬────────────┐
    #> │ fruits ┆ has_suffix │
    #> │ ---    ┆ ---        │
    #> │ str    ┆ bool       │
    #> ╞════════╪════════════╡
    #> │ apple  ┆ true       │
    #> │ mango  ┆ false      │
    #> │ null   ┆ null       │
    #> └────────┴────────────┘
