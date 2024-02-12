

# Get the last <code>n</code> rows.

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L272)

## Description

Get the last <code>n</code> rows.

## Usage

<pre><code class='language-R'>pl_tail(column, n = 10)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_tail_:_column">column</code>
</td>
<td>

if dtype is:

<ul>
<li>

Series: Take tail value in <code>Series</code>

</li>
<li>

str or in: syntactic sugar for
<code style="white-space: pre;">pl.col(..).tail()</code>

</li>
</ul>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_tail_:_n">n</code>
</td>
<td>
Number of rows to take
</td>
</tr>
</table>

## Value

Expr or tail value of input Series

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = c(1, 8, 3),
  b = c(4, 5, 2),
  c = c("foo", "bar", "foo")
)

expr_tail = pl$head("a")
print(expr_tail)
```

    #> polars Expr: col("a").slice(offset=0, length=10)

``` r
df$select(expr_tail)
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
df$select(pl$tail("a", 2))
```

    #> shape: (2, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ f64 │
    #> ╞═════╡
    #> │ 8.0 │
    #> │ 3.0 │
    #> └─────┘

``` r
pl$tail(df$get_column("a"), 2)
```

    #> polars Series: shape: (2,)
    #> Series: 'a' [f64]
    #> [
    #>  8.0
    #>  3.0
    #> ]
