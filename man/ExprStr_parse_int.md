

# Parse integers with base radix from strings

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__string.R#L830)

## Description

Parse integers with base 2 by default.

## Usage

<pre><code class='language-R'>ExprStr_parse_int(radix = 2, strict = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_parse_int_:_radix">radix</code>
</td>
<td>
Positive integer which is the base of the string we are parsing. Default
is 2.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_parse_int_:_strict">strict</code>
</td>
<td>
If <code>TRUE</code> (default), integer overflow will raise an error.
Otherwise, they will be converted to <code>null</code>.
</td>
</tr>
</table>

## Value

Expr: Series of dtype i32.

## Examples

``` r
library(polars)

df = pl$DataFrame(bin = c("110", "101", "010"))
df$select(pl$col("bin")$str$parse_int())
```

    #> shape: (3, 1)
    #> ┌─────┐
    #> │ bin │
    #> │ --- │
    #> │ i64 │
    #> ╞═════╡
    #> │ 6   │
    #> │ 5   │
    #> │ 2   │
    #> └─────┘

``` r
df$select(pl$col("bin")$str$parse_int(10))
```

    #> shape: (3, 1)
    #> ┌─────┐
    #> │ bin │
    #> │ --- │
    #> │ i64 │
    #> ╞═════╡
    #> │ 110 │
    #> │ 101 │
    #> │ 10  │
    #> └─────┘

``` r
# Convert to null if the string is not a valid integer when `strict = FALSE`
df = pl$DataFrame(x = c("1", "2", "foo"))
df$select(pl$col("x")$str$parse_int(10, FALSE))
```

    #> shape: (3, 1)
    #> ┌──────┐
    #> │ x    │
    #> │ ---  │
    #> │ i64  │
    #> ╞══════╡
    #> │ 1    │
    #> │ 2    │
    #> │ null │
    #> └──────┘
