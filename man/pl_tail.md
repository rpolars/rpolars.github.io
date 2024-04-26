

# Get the last <code>n</code> rows.

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L317)

## Description

This function is syntactic sugar for <code>pl$col(…)$tail(n)</code>.

## Usage

<pre><code class='language-R'>pl_tail(..., n = 10)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="...">…</code>
</td>
<td>
Characters indicating the column names, passed to <code>pl$col()</code>.
See <code>?pl_col</code> for details.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="n">n</code>
</td>
<td>
Number of rows to return.
</td>
</tr>
</table>

## Value

Expr

## See Also

<ul>
<li>

<code>\<Expr\>$tail()</code>

</li>
</ul>

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = c(1, 8, 3),
  b = c(4, 5, 2),
  c = c("foo", "bar", "foo")
)

df$select(pl$tail("a"))
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
df$select(pl$tail("a", "b", n = 2))
```

    #> shape: (2, 2)
    #> ┌─────┬─────┐
    #> │ a   ┆ b   │
    #> │ --- ┆ --- │
    #> │ f64 ┆ f64 │
    #> ╞═════╪═════╡
    #> │ 8.0 ┆ 5.0 │
    #> │ 3.0 ┆ 2.0 │
    #> └─────┴─────┘
