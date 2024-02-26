

# Get the median value.

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L338)

## Description

This function is syntactic sugar for <code>pl$col(…)$median()</code>.

## Usage

<pre><code class='language-R'>pl_median(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_median_:_...">…</code>
</td>
<td>
Characters indicating the column names, passed to <code>pl$col()</code>.
See <code>?pl_col</code> for details.
</td>
</tr>
</table>

## Value

Expr

## See Also

<ul>
<li>

<code>\<Expr\>$median()</code>

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

df$select(pl$median("a"))
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
df$select(pl$median("a", "b"))
```

    #> shape: (1, 2)
    #> ┌─────┬─────┐
    #> │ a   ┆ b   │
    #> │ --- ┆ --- │
    #> │ f64 ┆ f64 │
    #> ╞═════╪═════╡
    #> │ 3.0 ┆ 4.0 │
    #> └─────┴─────┘
