

# Aggregate all column values into a list.

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L199)

## Description

This function is syntactic sugar for <code>pl$col(…)$implode()</code>.

## Usage

<pre><code class='language-R'>pl_implode(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_implode_:_...">…</code>
</td>
<td>
Characters indicating the column names, passed to <code>pl$col()</code>.
See <code>?pl_col</code> for details.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(iris)$select(pl$implode("Species"))
```

    #> shape: (1, 1)
    #> ┌───────────────────────────────────┐
    #> │ Species                           │
    #> │ ---                               │
    #> │ list[cat]                         │
    #> ╞═══════════════════════════════════╡
    #> │ ["setosa", "setosa", … "virginic… │
    #> └───────────────────────────────────┘
