
# New Expr referring to all columns

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/functions__lazy.R#L15)

## Description

Not to mix up with <code>Expr_object$all()</code> which is a ‘reduce
Boolean columns by AND’ method.

## Usage

<pre><code class='language-R'>pl_all(name = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_all_:_name">name</code>
</td>
<td>
Character vector indicating on which columns the AND operation should be
applied.
</td>
</tr>
</table>

## Details

last <code>all()</code> in example is this Expr method, the first
<code>pl$all()</code> refers to "all-columns" and is an expression
constructor

## Value

Boolean literal

## Examples

``` r
library(polars)

pl$DataFrame(list(all = c(TRUE, TRUE), some = c(TRUE, FALSE)))$select(pl$all()$all())
```

    #> shape: (1, 2)
    #> ┌──────┬───────┐
    #> │ all  ┆ some  │
    #> │ ---  ┆ ---   │
    #> │ bool ┆ bool  │
    #> ╞══════╪═══════╡
    #> │ true ┆ false │
    #> └──────┴───────┘
