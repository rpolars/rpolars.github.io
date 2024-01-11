
# Compute sum in one or several columns

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L454)

## Description

This is syntactic sugar for <code>pl$col(…)$sum()</code>.

## Usage

<pre><code class='language-R'>pl_sum(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_sum_:_...">…</code>
</td>
<td>

One or several elements. Each element can be:

<ul>
<li>

Series or Expr

</li>
<li>

string, that is parsed as columns

</li>
<li>

numeric, that is parsed as literal

</li>
</ul>
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

# column as string
pl$DataFrame(iris)$select(pl$sum("Petal.Width"))
```

    #> shape: (1, 1)
    #> ┌─────────────┐
    #> │ Petal.Width │
    #> │ ---         │
    #> │ f64         │
    #> ╞═════════════╡
    #> │ 179.9       │
    #> └─────────────┘

``` r
# column as Expr (prefer pl$col("Petal.Width")$sum())
pl$DataFrame(iris)$select(pl$sum(pl$col("Petal.Width")))
```

    #> shape: (1, 1)
    #> ┌─────────────┐
    #> │ Petal.Width │
    #> │ ---         │
    #> │ f64         │
    #> ╞═════════════╡
    #> │ 179.9       │
    #> └─────────────┘

``` r
df = pl$DataFrame(a = 1:2, b = 3:4, c = 5:6)

# Compute sum in several columns
df$with_columns(pl$sum("*"))
```

    #> shape: (2, 3)
    #> ┌─────┬─────┬─────┐
    #> │ a   ┆ b   ┆ c   │
    #> │ --- ┆ --- ┆ --- │
    #> │ i32 ┆ i32 ┆ i32 │
    #> ╞═════╪═════╪═════╡
    #> │ 3   ┆ 7   ┆ 11  │
    #> │ 3   ┆ 7   ┆ 11  │
    #> └─────┴─────┴─────┘
