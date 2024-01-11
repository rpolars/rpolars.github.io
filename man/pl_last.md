
# pl$last

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L195)

## Description

Depending on the input type this function does different things:

## Usage

<pre><code class='language-R'>pl_last(column = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_last_:_column">column</code>
</td>
<td>

if dtype is:

<ul>
<li>

Series: Take last value in <code>Series</code>

</li>
<li>

str: syntactic sugar for
<code style="white-space: pre;">pl.col(..).last()</code>

</li>
<li>

NULL: expression to take last column of a context.

</li>
</ul>
</td>
</tr>
</table>

## Value

Expr or last value of input Series

## Examples

``` r
library(polars)


df = pl$DataFrame(
  a = c(1, 8, 3),
  b = c(4, 5, 2),
  c = c("foo", "bar", "foo")
)
df$select(pl$last())
```

    #> shape: (3, 1)
    #> ┌─────┐
    #> │ c   │
    #> │ --- │
    #> │ str │
    #> ╞═════╡
    #> │ foo │
    #> │ bar │
    #> │ foo │
    #> └─────┘

``` r
df$select(pl$last("a"))
```

    #> shape: (1, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ f64 │
    #> ╞═════╡
    #> │ 3.0 │
    #> └─────┘

``` r
pl$last(df$get_column("a"))
```

    #> [1] 3
