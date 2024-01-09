
# Vertically concatenate values of a Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/expr__string.R#L236)

## Description

Vertically concatenate the values in the Series to a single string
value.

## Usage

<pre><code class='language-R'>ExprStr_concat(delimiter = "-", ignore_nulls = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_concat_:_delimiter">delimiter</code>
</td>
<td>
The delimiter to insert between consecutive string values.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_concat_:_ignore_nulls">ignore_nulls</code>
</td>
<td>
Ignore null values. If <code>FALSE</code>, null values will be
propagated: if the column contains any null values, the output is null.
</td>
</tr>
</table>

## Value

Expr of String concatenated

## Examples

``` r
library(polars)

# concatenate a Series of strings to a single string
df = pl$DataFrame(foo = c("1", NA, 2))
df$select(pl$col("foo")$str$concat("-"))
```

    #> shape: (1, 1)
    #> ┌─────┐
    #> │ foo │
    #> │ --- │
    #> │ str │
    #> ╞═════╡
    #> │ 1-2 │
    #> └─────┘

``` r
df$select(pl$col("foo")$str$concat("-", ignore_nulls = FALSE))
```

    #> shape: (1, 1)
    #> ┌──────┐
    #> │ foo  │
    #> │ ---  │
    #> │ str  │
    #> ╞══════╡
    #> │ null │
    #> └──────┘

``` r
# Series list of strings to Series of concatenated strings
df = pl$DataFrame(list(bar = list(c("a", "b", "c"), c("1", "2", NA))))
df$select(pl$col("bar")$list$eval(pl$col()$str$concat())$list$first())
```

    #> shape: (2, 1)
    #> ┌───────┐
    #> │ bar   │
    #> │ ---   │
    #> │ str   │
    #> ╞═══════╡
    #> │ a-b-c │
    #> │ 1-2   │
    #> └───────┘
