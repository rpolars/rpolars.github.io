

# Get the standard deviation.

[**Source code**](https://github.com/pola-rs/r-polars/tree/mkdocs-matrial-search-preview/R/functions__lazy.R#L516)

## Description

This function is syntactic sugar for <code>pl$col(…)$std(ddof)</code>.

## Usage

<pre><code class='language-R'>pl_std(..., ddof = 1)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_std_:_...">…</code>
</td>
<td>
Characters indicating the column names, passed to <code>pl$col()</code>.
See <code>?pl_col</code> for details.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_std_:_ddof">ddof</code>
</td>
<td>
An integer representing "Delta Degrees of Freedom": the divisor used in
the calculation is <code>N - ddof</code>, where <code>N</code>
represents the number of elements. By default ddof is <code>1</code>.
</td>
</tr>
</table>

## Value

Expr

## See Also

<ul>
<li>

<code>\<Expr\>$std()</code>

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

df$select(pl$std("a"))
```

    #> shape: (1, 1)
    #> ┌──────────┐
    #> │ a        │
    #> │ ---      │
    #> │ f64      │
    #> ╞══════════╡
    #> │ 3.605551 │
    #> └──────────┘

``` r
df$select(pl$std(c("a", "b")))
```

    #> shape: (1, 2)
    #> ┌──────────┬──────────┐
    #> │ a        ┆ b        │
    #> │ ---      ┆ ---      │
    #> │ f64      ┆ f64      │
    #> ╞══════════╪══════════╡
    #> │ 3.605551 ┆ 1.527525 │
    #> └──────────┴──────────┘
