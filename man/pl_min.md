

# Find minimum value in one or several columns

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L494)

## Description

This is syntactic sugar for <code>pl$col(…)$min()</code>.

## Usage

<pre><code class='language-R'>pl_min(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_min_:_...">…</code>
</td>
<td>

is a: If one arg:

<ul>
<li>

Series or Expr, same as <code>column$sum()</code>

</li>
<li>

string, same as <code>pl$col(column)$sum()</code>

</li>
<li>

numeric, same as <code>pl$lit(column)$sum()</code>

</li>
<li>

list of strings(column names) or expressions to add up as expr1 +
expr2 + expr3 + … If several args, then wrapped in a list and handled as
above.

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

df = pl$DataFrame(
  a = NA_real_,
  b = c(1:2, NA_real_, NA_real_),
  c = c(1:4)
)
df
```

    #> shape: (4, 3)
    #> ┌──────┬──────┬─────┐
    #> │ a    ┆ b    ┆ c   │
    #> │ ---  ┆ ---  ┆ --- │
    #> │ f64  ┆ f64  ┆ i32 │
    #> ╞══════╪══════╪═════╡
    #> │ null ┆ 1.0  ┆ 1   │
    #> │ null ┆ 2.0  ┆ 2   │
    #> │ null ┆ null ┆ 3   │
    #> │ null ┆ null ┆ 4   │
    #> └──────┴──────┴─────┘
