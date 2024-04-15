

# Create Struct DataType

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/datatype.R#L253)

## Description

One can create a <code>Struct</code> data type with
<code>pl$Struct()</code>. There are also multiple ways to create columns
of data type <code>Struct</code> in a <code>DataFrame</code> or a
<code>Series</code>, see the examples.

## Usage

<pre><code class='language-R'>DataType_Struct(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataType_Struct_:_...">…</code>
</td>
<td>
RPolarsDataType objects
</td>
</tr>
</table>

## Value

a list DataType with an inner DataType

## Examples

``` r
library(polars)

# create a Struct-DataType
pl$Struct(pl$Boolean)
```

    #> DataType: Struct(
    #>     [
    #>         Field {
    #>             name: "",
    #>             dtype: Boolean,
    #>         },
    #>     ],
    #> )

``` r
pl$Struct(foo = pl$Int32, bar = pl$Float64)
```

    #> DataType: Struct(
    #>     [
    #>         Field {
    #>             name: "foo",
    #>             dtype: Int32,
    #>         },
    #>         Field {
    #>             name: "bar",
    #>             dtype: Float64,
    #>         },
    #>     ],
    #> )

``` r
# check if an element is any kind of Struct()
test = pl$Struct(pl$UInt64)
pl$same_outer_dt(test, pl$Struct())
```

    #> [1] TRUE

``` r
# `test` is a type of Struct, but it doesn't mean it is equal to an empty Struct
test == pl$Struct()
```

    #> [1] FALSE

``` r
# The way to create a `Series` of type `Struct` is a bit convoluted as it involves
# `data.frame()`, `list()`, and `I()`:
as_polars_series(
  data.frame(a = 1:2, b = I(list(c("x", "y"), "z")))
)
```

    #> polars Series: shape: (2,)
    #> Series: '' [struct[2]]
    #> [
    #>  {1,["x", "y"]}
    #>  {2,["z"]}
    #> ]

``` r
# A slightly simpler way would be via `tibble::tibble()` or
# `data.table::data.table()`:
if (requireNamespace("tibble", quietly = TRUE)) {
  as_polars_series(
    tibble::tibble(a = 1:2, b = list(c("x", "y"), "z"))
  )
}
```

    #> polars Series: shape: (2,)
    #> Series: '' [struct[2]]
    #> [
    #>  {1,["x", "y"]}
    #>  {2,["z"]}
    #> ]

``` r
# Finally, one can use the method `$to_struct()` to convert existing columns
# or `Series` to a `Struct`:
x = pl$DataFrame(
  a = 1:2,
  b = list(c("x", "y"), "z")
)

out = x$select(pl$col("a", "b")$to_struct())
out
```

    #> shape: (2, 1)
    #> ┌────────────────┐
    #> │ a              │
    #> │ ---            │
    #> │ struct[2]      │
    #> ╞════════════════╡
    #> │ {1,["x", "y"]} │
    #> │ {2,["z"]}      │
    #> └────────────────┘

``` r
out$schema
```

    #> $a
    #> DataType: Struct(
    #>     [
    #>         Field {
    #>             name: "a",
    #>             dtype: Int32,
    #>         },
    #>         Field {
    #>             name: "b",
    #>             dtype: List(
    #>                 String,
    #>             ),
    #>         },
    #>     ],
    #> )
