

# Add a prefix to all fields name of a struct

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/expr__name.R#L119)

## Description

Add a prefix to all fields name of a struct

## Usage

<pre><code class='language-R'>ExprName_prefix_fields(prefix)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprName_prefix_fields_:_prefix">prefix</code>
</td>
<td>
Prefix to add to the field name.
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

df$with_columns(pl$col("my_struct")$name$prefix_fields("col_"))$unnest()
```

    #> shape: (1, 2)
    #> ┌───────┬───────┐
    #> │ col_a ┆ col_b │
    #> │ ---   ┆ ---   │
    #> │ f64   ┆ f64   │
    #> ╞═══════╪═══════╡
    #> │ 1.0   ┆ 2.0   │
    #> └───────┴───────┘
