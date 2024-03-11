

# New Expr referring to all columns

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L53)

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

## Value

Boolean literal

## Examples

``` r
library(polars)

test = pl$DataFrame(col_1 = c(TRUE, TRUE), col_2 = c(TRUE, FALSE))
test
```

    #> shape: (2, 2)
    #> ┌───────┬───────┐
    #> │ col_1 ┆ col_2 │
    #> │ ---   ┆ ---   │
    #> │ bool  ┆ bool  │
    #> ╞═══════╪═══════╡
    #> │ true  ┆ true  │
    #> │ true  ┆ false │
    #> └───────┴───────┘

``` r
# here, the first `$all()` selects all columns, and the second `$all()` checks
# whether all values are true in each column
test$with_columns(pl$all()$all())
```

    #> shape: (2, 2)
    #> ┌───────┬───────┐
    #> │ col_1 ┆ col_2 │
    #> │ ---   ┆ ---   │
    #> │ bool  ┆ bool  │
    #> ╞═══════╪═══════╡
    #> │ true  ┆ false │
    #> │ true  ┆ false │
    #> └───────┴───────┘
