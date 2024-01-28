

# Repeat values

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/expr__expr.R#L2132)

## Description

Repeat the elements in this Series as specified in the given expression.
The repeated elements are expanded into a <code>List</code>.

## Usage

<pre><code class='language-R'>Expr_repeat_by(by)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_repeat_by_:_by">by</code>
</td>
<td>
Expr that determines how often the values will be repeated. The column
will be coerced to UInt32.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(a = c("w", "x", "y", "z"), n = c(-1, 0, 1, 2))
df$with_columns(repeated = pl$col("a")$repeat_by("n"))
```

    #> shape: (4, 3)
    #> ┌─────┬──────┬────────────┐
    #> │ a   ┆ n    ┆ repeated   │
    #> │ --- ┆ ---  ┆ ---        │
    #> │ str ┆ f64  ┆ list[str]  │
    #> ╞═════╪══════╪════════════╡
    #> │ w   ┆ -1.0 ┆ null       │
    #> │ x   ┆ 0.0  ┆ []         │
    #> │ y   ┆ 1.0  ┆ ["y"]      │
    #> │ z   ┆ 2.0  ┆ ["z", "z"] │
    #> └─────┴──────┴────────────┘
