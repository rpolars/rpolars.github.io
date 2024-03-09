

# Count unique values.

[**Source code**](https://github.com/pola-rs/r-polars/tree/mkdocs-matrial-search-preview/R/functions__lazy.R#L362)

## Description

This function is syntactic sugar for <code>pl$col(…)$n_unique()</code>.

## Usage

<pre><code class='language-R'>pl_n_unique(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_n_unique_:_...">…</code>
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

<code>\<Expr\>$n_unique()</code>

</li>
</ul>

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = c(1, 8, 1),
  b = c(4, 5, 2),
  c = c("foo", "bar", "foo")
)

df$select(pl$n_unique("a"))
```

    #> shape: (1, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ u32 │
    #> ╞═════╡
    #> │ 2   │
    #> └─────┘

``` r
df$select(pl$n_unique("b", "c"))
```

    #> shape: (1, 2)
    #> ┌─────┬─────┐
    #> │ b   ┆ c   │
    #> │ --- ┆ --- │
    #> │ u32 ┆ u32 │
    #> ╞═════╪═════╡
    #> │ 3   ┆ 2   │
    #> └─────┴─────┘
