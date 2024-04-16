

# Convert array to struct

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__array.R#L314)

## Description

Convert array to struct

## Usage

<pre><code class='language-R'>ExprArr_to_struct(fields = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprArr_to_struct_:_fields">fields</code>
</td>
<td>
If the name and number of the desired fields is known in advance, a list
of field names can be given, which will be assigned by index. Otherwise,
to dynamically assign field names, a custom R function that takes an R
double and outputs a string value can be used. If <code>NULL</code>
(default), fields will be <code>field_0</code>, <code>field_1</code> …
<code>field_n</code>.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(
  values = list(1:3, c(2L, NA_integer_, 5L)),
  schema = list(values = pl$Array(pl$Int32, 3))
)
df$with_columns(
  struct = pl$col("values")$arr$to_struct()
)
```

    #> shape: (2, 2)
    #> ┌───────────────┬────────────┐
    #> │ values        ┆ struct     │
    #> │ ---           ┆ ---        │
    #> │ array[i32, 3] ┆ struct[3]  │
    #> ╞═══════════════╪════════════╡
    #> │ [1, 2, 3]     ┆ {1,2,3}    │
    #> │ [2, null, 5]  ┆ {2,null,5} │
    #> └───────────────┴────────────┘

``` r
# pass a custom function that will name all fields by adding a prefix
df2 = df$with_columns(
  pl$col("values")$arr$to_struct(
    fields = \(idx) paste0("col_", idx)
  )
)
df2
```

    #> shape: (2, 1)
    #> ┌────────────┐
    #> │ values     │
    #> │ ---        │
    #> │ struct[3]  │
    #> ╞════════════╡
    #> │ {1,2,3}    │
    #> │ {2,null,5} │
    #> └────────────┘

``` r
df2$unnest()
```

    #> shape: (2, 3)
    #> ┌───────┬───────┬───────┐
    #> │ col_0 ┆ col_1 ┆ col_2 │
    #> │ ---   ┆ ---   ┆ ---   │
    #> │ i32   ┆ i32   ┆ i32   │
    #> ╞═══════╪═══════╪═══════╡
    #> │ 1     ┆ 2     ┆ 3     │
    #> │ 2     ┆ null  ┆ 5     │
    #> └───────┴───────┴───────┘
