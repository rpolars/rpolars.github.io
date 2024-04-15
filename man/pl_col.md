

# Create an expression representing column(s) in a dataframe

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/functions__lazy.R#L100)

## Description

Create an expression representing column(s) in a dataframe

## Usage

<pre><code class='language-R'>pl_col(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_col_:_...">…</code>
</td>
<td>

One of the following:

<ul>
<li>

character vectors

<ul>
<li>

Single wildcard <code>“\*“</code> has a special meaning: check the
examples.

</li>
</ul>
</li>
<li>

RPolarsDataTypes

</li>
<li>

a list of RPolarsDataTypes

</li>
</ul>
</td>
</tr>
</table>

## Value

Expr of a column or columns

## Examples

``` r
library(polars)

# a single column by a character
pl$col("foo")
```

    #> polars Expr: col("foo")

``` r
# multiple columns by characters
pl$col("foo", "bar")
```

    #> polars Expr: cols(["foo", "bar"])

``` r
# multiple columns by RPolarsDataTypes
pl$col(pl$Float64, pl$String)
```

    #> polars Expr: dtype_columns([Float64, String])

``` r
# Single `"*"` is converted to a wildcard expression
pl$col("*")
```

    #> polars Expr: *

``` r
# multiple character vectors and a list of RPolarsDataTypes are also allowed
pl$col(c("foo", "bar"), "baz")
```

    #> polars Expr: cols(["foo", "bar", "baz"])

``` r
pl$col("foo", c("bar", "baz"))
```

    #> polars Expr: cols(["foo", "bar", "baz"])

``` r
pl$col(list(pl$Float64, pl$String))
```

    #> polars Expr: dtype_columns([Float64, String])

``` r
# there are some special notations for selecting columns
df = pl$DataFrame(foo = 1:3, bar = 4:6, baz = 7:9)

# select all columns with a wildcard `"*"`
df$select(pl$col("*"))
```

    #> shape: (3, 3)
    #> ┌─────┬─────┬─────┐
    #> │ foo ┆ bar ┆ baz │
    #> │ --- ┆ --- ┆ --- │
    #> │ i32 ┆ i32 ┆ i32 │
    #> ╞═════╪═════╪═════╡
    #> │ 1   ┆ 4   ┆ 7   │
    #> │ 2   ┆ 5   ┆ 8   │
    #> │ 3   ┆ 6   ┆ 9   │
    #> └─────┴─────┴─────┘

``` r
# select multiple columns by a regular expression
# starts with `^` and ends with `$`
df$select(pl$col(c("^ba.*$")))
```

    #> shape: (3, 2)
    #> ┌─────┬─────┐
    #> │ bar ┆ baz │
    #> │ --- ┆ --- │
    #> │ i32 ┆ i32 │
    #> ╞═════╪═════╡
    #> │ 4   ┆ 7   │
    #> │ 5   ┆ 8   │
    #> │ 6   ┆ 9   │
    #> └─────┴─────┘
