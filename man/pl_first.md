

# pl$first

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/functions__lazy.R#L155)

## Description

Depending on the input type this function does different things:

## Usage

<pre><code class='language-R'>pl_first(column = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_first_:_column">column</code>
</td>
<td>

if dtype is:

<ul>
<li>

Series: Take first value in <code>Series</code>

</li>
<li>

str: syntactic sugar for
<code style="white-space: pre;">pl.col(..).first()</code>

</li>
<li>

NULL: expression to take first column of a context.

</li>
</ul>
</td>
</tr>
</table>

## Value

Expr or first value of input Series

## Examples

``` r
library(polars)


df = pl$DataFrame(
  a = c(1, 8, 3),
  b = c(4, 5, 2),
  c = c("foo", "bar", "foo")
)
df$select(pl$first())
```

    #> shape: (3, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ f64 │
    #> ╞═════╡
    #> │ 1.0 │
    #> │ 8.0 │
    #> │ 3.0 │
    #> └─────┘

``` r
df$select(pl$first("a"))
```

    #> shape: (1, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ f64 │
    #> ╞═════╡
    #> │ 1.0 │
    #> └─────┘

``` r
pl$first(df$get_column("a"))
```

    #> [1] 1
