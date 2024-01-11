
# Get the first <code>n</code> rows.

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L232)

## Description

Get the first <code>n</code> rows.

## Usage

<pre><code class='language-R'>pl_head(column, n = 10)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_head_:_column">column</code>
</td>
<td>

if dtype is:

<ul>
<li>

Series: Take head value in <code>Series</code>

</li>
<li>

str or int: syntactic sugar for
<code style="white-space: pre;">pl.col(..).head()</code>

</li>
</ul>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_head_:_n">n</code>
</td>
<td>
Number of rows to take
</td>
</tr>
</table>

## Value

Expr or head value of input Series

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = c(1, 8, 3),
  b = c(4, 5, 2),
  c = c("foo", "bar", "foo")
)

expr_head = pl$head("a")
print(expr_head)
```

    #> polars Expr: col("a").slice(offset=0, length=10)

``` r
df$select(expr_head)
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
df$select(pl$head("a", 2))
```

    #> shape: (2, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ f64 │
    #> ╞═════╡
    #> │ 1.0 │
    #> │ 8.0 │
    #> └─────┘

``` r
pl$head(df$get_column("a"), 2)
```

    #> polars Series: shape: (2,)
    #> Series: 'a' [f64]
    #> [
    #>  1.0
    #>  8.0
    #> ]
