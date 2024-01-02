
# pl$median

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/functions__lazy.R#L343)

## Description

Depending on the input type this function does different things:

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

Expr or median value of input Series

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
