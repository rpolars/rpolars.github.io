

# struct

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L719)

## Description

Collect several columns into a Series of dtype Struct.

## Usage

<pre><code class='language-R'>pl_struct(exprs, eager = FALSE, schema = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_struct_:_exprs">exprs</code>
</td>
<td>
Columns/Expressions to collect into a Struct.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_struct_:_eager">eager</code>
</td>
<td>
Evaluate immediately.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_struct_:_schema">schema</code>
</td>
<td>
Optional schema named list that explicitly defines the struct field
dtypes. Each name must match a column name wrapped in the struct. Can
only be used to cast some or all dtypes, not to change the names. NULL
means to include keep columns into the struct by their current DataType.
If a column is not included in the schema it is removed from the final
struct.
</td>
</tr>
</table>

## Details

pl$struct creates Expr or Series of DataType Struct() pl$Struct creates
the DataType Struct() In polars a schema is a named list of DataTypes.
#’ A schema describes e.g. a DataFrame. More formally schemas consist of
Fields. A Field is an object describing the name and DataType of a
column/Series, but same same. A struct is a DataFrame wrapped into a
Series, the DataType is Struct, and each sub-datatype within are Fields.
In a dynamic language schema and a Struct (the DataType) are quite the
same, except schemas describe DataFrame and Struct’s describe some
Series.

## Value

Eager=FALSE: Expr of Series with dtype Struct | Eager=TRUE: Series with
dtype Struct

## Examples

``` r
library(polars)

# isolated expression to wrap all columns in a struct aliased 'my_struct'
pl$struct(pl$all())$alias("my_struct")
```

    #> polars Expr: *.as_struct().alias("my_struct")

``` r
# wrap all column into on column/Series
df = pl$DataFrame(
  int = 1:2,
  str = c("a", "b"),
  bool = c(TRUE, NA),
  list = list(1:2, 3L)
)$select(
  pl$struct(pl$all())$alias("my_struct")
)

print(df)
```

    #> shape: (2, 1)
    #> ┌─────────────────────┐
    #> │ my_struct           │
    #> │ ---                 │
    #> │ struct[4]           │
    #> ╞═════════════════════╡
    #> │ {1,"a",true,[1, 2]} │
    #> │ {2,"b",null,[3]}    │
    #> └─────────────────────┘

``` r
print(df$schema) # returns a schema, a named list containing one element a Struct named my_struct
```

    #> $my_struct
    #> DataType: Struct(
    #>     [
    #>         Field {
    #>             name: "int",
    #>             dtype: Int32,
    #>         },
    #>         Field {
    #>             name: "str",
    #>             dtype: String,
    #>         },
    #>         Field {
    #>             name: "bool",
    #>             dtype: Boolean,
    #>         },
    #>         Field {
    #>             name: "list",
    #>             dtype: List(
    #>                 Int32,
    #>             ),
    #>         },
    #>     ],
    #> )

``` r
# wrap two columns in a struct and provide a schema to set all or some DataTypes by name
e1 = pl$struct(
  pl$col(c("int", "str")),
  schema = list(int = pl$Int64, str = pl$String)
)$alias("my_struct")
# same result as e.g. wrapping the columns in a struct and casting afterwards
e2 = pl$struct(
  list(pl$col("int"), pl$col("str"))
)$cast(
  pl$Struct(int = pl$Int64, str = pl$String)
)$alias("my_struct")

df = pl$DataFrame(
  int = 1:2,
  str = c("a", "b"),
  bool = c(TRUE, NA),
  list = list(1:2, 3L)
)

# verify equality in R
identical(df$select(e1)$to_list(), df$select(e2)$to_list())
```

    #> [1] TRUE

``` r
df$select(e2)
```

    #> shape: (2, 1)
    #> ┌───────────┐
    #> │ my_struct │
    #> │ ---       │
    #> │ struct[2] │
    #> ╞═══════════╡
    #> │ {1,"a"}   │
    #> │ {2,"b"}   │
    #> └───────────┘

``` r
df$select(e2)$to_data_frame()
```

    #>   my_struct
    #> 1      1, a
    #> 2      2, b
