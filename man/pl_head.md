

# Get the first <code>n</code> rows.

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/functions__lazy.R#L294)

## Description

This function is syntactic sugar for <code>pl$col(…)$head(n)</code>.

## Usage

<pre><code class='language-R'>pl_head(..., n = 10)
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

<code>\<Expr\>$head()</code>

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

df$select(pl$head("a"))
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
df$select(pl$head("a", "b", n = 2))
```

    #> shape: (2, 2)
    #> ┌─────┬─────┐
    #> │ a   ┆ b   │
    #> │ --- ┆ --- │
    #> │ f64 ┆ f64 │
    #> ╞═════╪═════╡
    #> │ 1.0 ┆ 4.0 │
    #> │ 8.0 ┆ 5.0 │
    #> └─────┴─────┘
