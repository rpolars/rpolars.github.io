
# rename fields

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__struct.R#L49)

## Description

Rename the fields of the struct. By default base 2.

## Usage

<pre><code class='language-R'>ExprStruct_rename_fields(names)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStruct_rename_fields_:_names">names</code>
</td>
<td>
char vec or list of strings given in the same order as the struct’s
fields. Providing fewer names will drop the latter fields. Providing too
many names is ignored.
</td>
</tr>
</table>

## Value

Expr: struct-series with new names for the fields

## Examples

``` r
library(polars)

df = pl$DataFrame(
  aaa = 1:2,
  bbb = c("ab", "cd"),
  ccc = c(TRUE, NA),
  ddd = list(1:2, 3L)
)$select(
  pl$struct(pl$all())$alias("struct_col")
)$select(
  pl$col("struct_col")$struct$rename_fields(c("www", "xxx", "yyy", "zzz"))
)
df$unnest()
```

    #> shape: (2, 4)
    #> ┌─────┬─────┬──────┬───────────┐
    #> │ www ┆ xxx ┆ yyy  ┆ zzz       │
    #> │ --- ┆ --- ┆ ---  ┆ ---       │
    #> │ i32 ┆ str ┆ bool ┆ list[i32] │
    #> ╞═════╪═════╪══════╪═══════════╡
    #> │ 1   ┆ ab  ┆ true ┆ [1, 2]    │
    #> │ 2   ┆ cd  ┆ null ┆ [3]       │
    #> └─────┴─────┴──────┴───────────┘
