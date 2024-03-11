

# Add a suffix to all fields name of a struct

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/expr__name.R#L136)

## Description

Add a suffix to all fields name of a struct

## Usage

<pre><code class='language-R'>ExprName_suffix_fields(suffix)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprName_suffix_fields_:_suffix">suffix</code>
</td>
<td>
Suffix to add to the field name.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(a = 1, b = 2)$select(
  pl$struct(pl$all())$alias("my_struct")
)

df$with_columns(pl$col("my_struct")$name$suffix_fields("_post"))$unnest()
```

    #> shape: (1, 2)
    #> ┌────────┬────────┐
    #> │ a_post ┆ b_post │
    #> │ ---    ┆ ---    │
    #> │ f64    ┆ f64    │
    #> ╞════════╪════════╡
    #> │ 1.0    ┆ 2.0    │
    #> └────────┴────────┘
