

# Get the first value.

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L229)

## Description

This function has different behavior depending on arguments:

<ul>
<li>

Missing -\> Takes first column of a context.

</li>
<li>

Character vectors -\> Syntactic sugar for
<code>pl$col(…)$first()</code>.

</li>
</ul>

## Usage

<pre><code class='language-R'>pl_first(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_first_:_...">…</code>
</td>
<td>
Characters indicating the column names (passed to <code>pl$col()</code>,
see <code>?pl_col</code> for details), or empty. If empty (default),
returns an expression to take the first column of the context instead.
</td>
</tr>
</table>

## Value

Expr

## See Also

<ul>
<li>

<code>\<Expr\>$first()</code>

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
df$select(pl$first("b"))
```

    #> shape: (1, 1)
    #> ┌─────┐
    #> │ b   │
    #> │ --- │
    #> │ f64 │
    #> ╞═════╡
    #> │ 4.0 │
    #> └─────┘

``` r
df$select(pl$first(c("a", "c")))
```

    #> shape: (1, 2)
    #> ┌─────┬─────┐
    #> │ a   ┆ c   │
    #> │ --- ┆ --- │
    #> │ f64 ┆ str │
    #> ╞═════╪═════╡
    #> │ 1.0 ┆ foo │
    #> └─────┴─────┘
