

# Return indices that match a condition

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/functions__lazy.R#L1233)

## Description

Return indices that match a condition

## Usage

<pre><code class='language-R'>pl_arg_where(condition)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_arg_where_:_condition">condition</code>
</td>
<td>
An Expr that gives a boolean.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(a = c(1, 2, 3, 4, 5))
df$select(
  pl$arg_where(pl$col("a") %% 2 == 0)
)
```

    #> shape: (2, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ u32 │
    #> ╞═════╡
    #> │ 1   │
    #> │ 3   │
    #> └─────┘
