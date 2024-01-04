
# pl$mean

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L304)

## Description

Depending on the input type this function does different things:

## Usage

<pre><code class='language-R'>pl_mean(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_mean_:_...">…</code>
</td>
<td>

One or several elements:

<ul>
<li>

Series: Take mean value in <code>Series</code>

</li>
<li>

DataFrame or LazyFrame: Take mean value of each column

</li>
<li>

character vector: parsed as column names

</li>
<li>

NULL: expression to take mean column of a context.

</li>
</ul>
</td>
</tr>
</table>

## Value

Expr or mean value of input Series

## Examples

``` r
library(polars)


df = pl$DataFrame(
  a = c(1, 8, 3),
  b = c(4, 5, 2),
  c = c("foo", "bar", "foo")
)
df$select(pl$mean("a"))
```

    #> shape: (1, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ f64 │
    #> ╞═════╡
    #> │ 4.0 │
    #> └─────┘

``` r
df$select(pl$mean("a", "b"))
```

    #> shape: (1, 2)
    #> ┌─────┬──────────┐
    #> │ a   ┆ b        │
    #> │ --- ┆ ---      │
    #> │ f64 ┆ f64      │
    #> ╞═════╪══════════╡
    #> │ 4.0 ┆ 3.666667 │
    #> └─────┴──────────┘
