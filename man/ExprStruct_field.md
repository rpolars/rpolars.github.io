

# field

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/expr__struct.R#L23)

## Description

Retrieve a <code>Struct</code> field as a new Series. By default base 2.

## Usage

<pre><code class='language-R'>ExprStruct_field(name)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStruct_field_:_name">name</code>
</td>
<td>
string, the Name of the struct field to retrieve.
</td>
</tr>
</table>

## Value

Expr: Series of same and name selected field.

## Examples

``` r
library(polars)

df = pl$DataFrame(
  aaa = c(1, 2),
  bbb = c("ab", "cd"),
  ccc = c(TRUE, NA),
  ddd = list(c(1, 2), 3)
)$select(
  pl$struct(pl$all())$alias("struct_col")
)
# struct field into a new Series
df$select(
  pl$col("struct_col")$struct$field("bbb"),
  pl$col("struct_col")$struct$field("ddd")
)
```

    #> shape: (2, 2)
    #> ┌─────┬────────────┐
    #> │ bbb ┆ ddd        │
    #> │ --- ┆ ---        │
    #> │ str ┆ list[f64]  │
    #> ╞═════╪════════════╡
    #> │ ab  ┆ [1.0, 2.0] │
    #> │ cd  ┆ [3.0]      │
    #> └─────┴────────────┘
