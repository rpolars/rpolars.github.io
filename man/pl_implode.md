
# Aggregate all column values into a list.

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L125)

## Description

Aggregate all column values into a list.

## Usage

<pre><code class='language-R'>pl_implode(name)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_implode_:_name">name</code>
</td>
<td>
Name of the column(s) that should be imploded, passed to pl$col()
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
