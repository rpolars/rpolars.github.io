

# Add a prefix to all fields name of a struct

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/expr__name.R#L119)

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
