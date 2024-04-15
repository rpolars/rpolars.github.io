

# Get the last value.

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/functions__lazy.R#L264)

## Description

This function has different behavior depending on the input type:

<ul>
<li>

Missing -\> Takes last column of a context.

</li>
<li>

Character vectors -\> Syntactic sugar for <code>pl$col(…)$last()</code>.

</li>
</ul>

## Usage

<pre><code class='language-R'>pl_last(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_last_:_...">…</code>
</td>
<td>
Characters indicating the column names (passed to <code>pl$col()</code>,
see <code>?pl_col</code> for details), or empty. If empty (default),
returns an expression to take the last column of the context instead.
</td>
</tr>
</table>

## Value

Expr

## See Also

<ul>
<li>

<code>\<Expr\>$last()</code>

</li>
</ul>

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = c(1, 8, 3),
  b = c(4, 5, 2),
  c = c("foo", "bar", "baz")
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
    #> │ baz │
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
df$select(pl$last(c("b", "c")))
```

    #> shape: (1, 2)
    #> ┌─────┬─────┐
    #> │ b   ┆ c   │
    #> │ --- ┆ --- │
    #> │ f64 ┆ str │
    #> ╞═════╪═════╡
    #> │ 2.0 ┆ baz │
    #> └─────┴─────┘
