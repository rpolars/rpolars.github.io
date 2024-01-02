
# Split the string by a substring

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/expr__string.R#L676)

## Description

Split the string by a substring

## Usage

<pre><code class='language-R'>ExprStr_split(by, inclusive = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_split_:_by">by</code>
</td>
<td>
String or Expr of a string, a valid regex pattern that will be used to
split the string.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_split_:_inclusive">inclusive</code>
</td>
<td>
If <code>TRUE</code>, include the split character/string in the results.
</td>
</tr>
</table>

## Value

List of Utf8 type

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
