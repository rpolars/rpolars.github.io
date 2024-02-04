

# Start Expression with a column

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L70)

## Description

Return an expression representing a column in a DataFrame.

## Usage

<pre><code class='language-R'>pl_col(name = "", ...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_col_:_name">name</code>
</td>
<td>
<ul>
<li>

a single column by a string

</li>
<li>

all columns by using a wildcard <code>“\*“</code>

</li>
<li>

multiple columns as vector of strings

</li>
<li>

column by regular expression if the regex starts with <code>^</code> and
ends with <code>$</code>
e.g. pl$DataFrame(iris)$select(pl$col(c("^Sepal.\*$")))

</li>
<li>

a single DataType or an R list of DataTypes, select any column of any
such DataType

</li>
<li>

Series of utf8 strings abiding to above options

</li>
</ul>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_col_:_...">…</code>
</td>
<td>
Additional column names can be passed as strings, separated by commas.
</td>
</tr>
</table>

## Value

Column Expression

## Examples

``` r
library(polars)


df = pl$DataFrame(list(foo = 1, bar = 2L, foobar = "3"))

# a single column by a string
df$select(pl$col("foo"))
```

    #> shape: (1, 1)
    #> ┌─────┐
    #> │ foo │
    #> │ --- │
    #> │ f64 │
    #> ╞═════╡
    #> │ 1.0 │
    #> └─────┘

``` r
# two columns as strings separated by commas
df$select(pl$col("foo", "bar"))
```

    #> shape: (1, 2)
    #> ┌─────┬─────┐
    #> │ foo ┆ bar │
    #> │ --- ┆ --- │
    #> │ f64 ┆ i32 │
    #> ╞═════╪═════╡
    #> │ 1.0 ┆ 2   │
    #> └─────┴─────┘

``` r
# all columns by wildcard
df$select(pl$col("*"))
```

    #> shape: (1, 3)
    #> ┌─────┬─────┬────────┐
    #> │ foo ┆ bar ┆ foobar │
    #> │ --- ┆ --- ┆ ---    │
    #> │ f64 ┆ i32 ┆ str    │
    #> ╞═════╪═════╪════════╡
    #> │ 1.0 ┆ 2   ┆ 3      │
    #> └─────┴─────┴────────┘

``` r
df$select(pl$all())
```

    #> shape: (1, 3)
    #> ┌─────┬─────┬────────┐
    #> │ foo ┆ bar ┆ foobar │
    #> │ --- ┆ --- ┆ ---    │
    #> │ f64 ┆ i32 ┆ str    │
    #> ╞═════╪═════╪════════╡
    #> │ 1.0 ┆ 2   ┆ 3      │
    #> └─────┴─────┴────────┘

``` r
# multiple columns as vector of strings
df$select(pl$col(c("foo", "bar")))
```

    #> shape: (1, 2)
    #> ┌─────┬─────┐
    #> │ foo ┆ bar │
    #> │ --- ┆ --- │
    #> │ f64 ┆ i32 │
    #> ╞═════╪═════╡
    #> │ 1.0 ┆ 2   │
    #> └─────┴─────┘

``` r
# column by regular expression if the regex starts with `^` and ends with `$`
df$select(pl$col("^foo.*$"))
```

    #> shape: (1, 2)
    #> ┌─────┬────────┐
    #> │ foo ┆ foobar │
    #> │ --- ┆ ---    │
    #> │ f64 ┆ str    │
    #> ╞═════╪════════╡
    #> │ 1.0 ┆ 3      │
    #> └─────┴────────┘

``` r
# a single DataType
df$select(pl$col(pl$dtypes$Float64))
```

    #> shape: (1, 1)
    #> ┌─────┐
    #> │ foo │
    #> │ --- │
    #> │ f64 │
    #> ╞═════╡
    #> │ 1.0 │
    #> └─────┘

``` r
# ... or an R list of DataTypes, select any column of any such DataType
df$select(pl$col(list(pl$dtypes$Float64, pl$dtypes$String)))
```

    #> shape: (1, 2)
    #> ┌─────┬────────┐
    #> │ foo ┆ foobar │
    #> │ --- ┆ ---    │
    #> │ f64 ┆ str    │
    #> ╞═════╪════════╡
    #> │ 1.0 ┆ 3      │
    #> └─────┴────────┘

``` r
# from Series of names
df$select(pl$col(pl$Series(c("bar", "foobar"))))
```

    #> shape: (1, 2)
    #> ┌─────┬────────┐
    #> │ bar ┆ foobar │
    #> │ --- ┆ ---    │
    #> │ i32 ┆ str    │
    #> ╞═════╪════════╡
    #> │ 2   ┆ 3      │
    #> └─────┴────────┘
