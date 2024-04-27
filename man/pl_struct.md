

# Collect columns into a struct column

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L656)

## Description

Collect columns into a struct column

## Usage

<pre><code class='language-R'>pl_struct(exprs, schema = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="exprs">exprs</code>
</td>
<td>
Columns/Expressions to collect into a Struct.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="schema">schema</code>
</td>
<td>
Optional schema named list that explicitly defines the struct field
dtypes. Each name must match a column name wrapped in the struct. Can
only be used to cast some or all dtypes, not to change the names. If
<code>NULL</code> (default), columns datatype are not modified. Columns
that do not exist are silently ignored and not included in the final
struct.
</td>
</tr>
</table>

## Details

<code>pl$struct()</code> creates an Expr of DataType
<code>Struct()</code>.

Compared to the Python implementation, <code>pl$struct()</code> doesn’t
have the argument <code>eager</code> and always returns an Expr. Use
<code style="white-space: pre;">$to_series()</code> to return a Series.

## Value

Expr with dtype Struct

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
