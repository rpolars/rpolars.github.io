

# Get the variance.

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/functions__lazy.R#L559)

## Description

This function is syntactic sugar for <code>pl$col(…)$var(ddof)</code>.

## Usage

<pre><code class='language-R'>pl_var(..., ddof = 1)
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
<code id="ddof">ddof</code>
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

<code>\<Expr\>$var()</code>

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

df$select(pl$var("a"))
```

    #> shape: (1, 1)
    #> ┌──────┐
    #> │ a    │
    #> │ ---  │
    #> │ f64  │
    #> ╞══════╡
    #> │ 13.0 │
    #> └──────┘

``` r
df$select(pl$var("a", "b"))
```

    #> shape: (1, 2)
    #> ┌──────┬──────────┐
    #> │ a    ┆ b        │
    #> │ ---  ┆ ---      │
    #> │ f64  ┆ f64      │
    #> ╞══════╪══════════╡
    #> │ 13.0 ┆ 2.333333 │
    #> └──────┴──────────┘
