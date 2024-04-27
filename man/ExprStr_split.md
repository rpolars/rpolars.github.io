

# Split the string by a substring

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__string.R#L699)

## Description

Split the string by a substring

## Usage

<pre><code class='language-R'>ExprStr_split(by, inclusive = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="by">by</code>
</td>
<td>
Substring to split by. Can be an Expr.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="inclusive">inclusive</code>
</td>
<td>
If <code>TRUE</code>, include the split character/string in the results.
</td>
</tr>
</table>

## Value

List of String type

## Examples

``` r
library(polars)

df = pl$DataFrame(s = c("foo bar", "foo-bar", "foo bar baz"))
df$select(pl$col("s")$str$split(by = " "))
```

    #> shape: (3, 1)
    #> ┌───────────────────────┐
    #> │ s                     │
    #> │ ---                   │
    #> │ list[str]             │
    #> ╞═══════════════════════╡
    #> │ ["foo", "bar"]        │
    #> │ ["foo-bar"]           │
    #> │ ["foo", "bar", "baz"] │
    #> └───────────────────────┘

``` r
df = pl$DataFrame(
  s = c("foo^bar", "foo_bar", "foo*bar*baz"),
  by = c("_", "_", "*")
)
df
```

    #> shape: (3, 2)
    #> ┌─────────────┬─────┐
    #> │ s           ┆ by  │
    #> │ ---         ┆ --- │
    #> │ str         ┆ str │
    #> ╞═════════════╪═════╡
    #> │ foo^bar     ┆ _   │
    #> │ foo_bar     ┆ _   │
    #> │ foo*bar*baz ┆ *   │
    #> └─────────────┴─────┘

``` r
df$select(pl$col("s")$str$split(by = pl$col("by"))$alias("split"))
```

    #> shape: (3, 1)
    #> ┌───────────────────────┐
    #> │ split                 │
    #> │ ---                   │
    #> │ list[str]             │
    #> ╞═══════════════════════╡
    #> │ ["foo^bar"]           │
    #> │ ["foo", "bar"]        │
    #> │ ["foo", "bar", "baz"] │
    #> └───────────────────────┘
