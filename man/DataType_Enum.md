

# Create Enum DataType

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/datatype.R#L415)

## Description

An <code>Enum</code> is a fixed set categorical encoding of a set of
strings. It is similar to the <code>Categorical</code> data type, but
the categories are explicitly provided by the user and cannot be
modified.

## Usage

<pre><code class='language-R'>DataType_Enum(categories)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="categories">categories</code>
</td>
<td>
A character vector specifying the categories of the variable.
</td>
</tr>
</table>

## Details

This functionality is <strong>unstable</strong>. It is a
work-in-progress feature and may not always work as expected. It may be
changed at any point without it being considered a breaking change.

## Value

An Enum DataType

## Examples

``` r
library(polars)

pl$DataFrame(
  x = c("Polar", "Panda", "Brown", "Brown", "Polar"),
  schema = list(x = pl$Enum(c("Polar", "Panda", "Brown")))
)
```

    #> shape: (5, 1)
    #> ┌───────┐
    #> │ x     │
    #> │ ---   │
    #> │ enum  │
    #> ╞═══════╡
    #> │ Polar │
    #> │ Panda │
    #> │ Brown │
    #> │ Brown │
    #> │ Polar │
    #> └───────┘

``` r
# All values of the variable have to be in the categories
dtype = pl$Enum(c("Polar", "Panda", "Brown"))
tryCatch(
  pl$DataFrame(
    x = c("Polar", "Panda", "Brown", "Brown", "Polar", "Black"),
    schema = list(x = dtype)
  ),
  error = function(e) e
)
```

    #> <RPolarsErr_error: Execution halted with the following contexts
    #>    0: In R: in $DataFrame():
    #>    0: During function call [.main()]
    #>    1: Encountered the following error in Rust-Polars:
    #>          conversion from `str` to `enum` failed in column '' for 1 out of 6 values: ["Black"]
    #> 
    #>       Ensure that all values in the input column are present in the categories of the enum datatype.
    #> >

``` r
# Comparing two Enum is only valid if they have the same categories
df = pl$DataFrame(
  x = c("Polar", "Panda", "Brown", "Brown", "Polar"),
  y = c("Polar", "Polar", "Polar", "Brown", "Brown"),
  z = c("Polar", "Polar", "Polar", "Brown", "Brown"),
  schema = list(
    x = pl$Enum(c("Polar", "Panda", "Brown")),
    y = pl$Enum(c("Polar", "Panda", "Brown")),
    z = pl$Enum(c("Polar", "Black", "Brown"))
  )
)

# Same categories
df$with_columns(x_eq_y = pl$col("x") == pl$col("y"))
```

    #> shape: (5, 4)
    #> ┌───────┬───────┬───────┬────────┐
    #> │ x     ┆ y     ┆ z     ┆ x_eq_y │
    #> │ ---   ┆ ---   ┆ ---   ┆ ---    │
    #> │ enum  ┆ enum  ┆ enum  ┆ bool   │
    #> ╞═══════╪═══════╪═══════╪════════╡
    #> │ Polar ┆ Polar ┆ Polar ┆ true   │
    #> │ Panda ┆ Polar ┆ Polar ┆ false  │
    #> │ Brown ┆ Polar ┆ Polar ┆ false  │
    #> │ Brown ┆ Brown ┆ Brown ┆ true   │
    #> │ Polar ┆ Brown ┆ Brown ┆ false  │
    #> └───────┴───────┴───────┴────────┘

``` r
# Different categories
tryCatch(
  df$with_columns(x_eq_z = pl$col("x") == pl$col("z")),
  error = function(e) e
)
```

    #> <RPolarsErr_error: Execution halted with the following contexts
    #>    0: In R: in $with_columns()
    #>    0: During function call [.main()]
    #>    1: Encountered the following error in Rust-Polars:
    #>          string caches don't match: cannot compare categoricals coming from different sources, consider setting a global StringCache.
    #> 
    #>       Help: if you're using Python, this may look something like:
    #> 
    #>           with pl.StringCache():
    #>               # Initialize Categoricals.
    #>               df1 = pl.DataFrame({'a': ['1', '2']}, schema={'a': pl.Categorical})
    #>               df2 = pl.DataFrame({'a': ['1', '3']}, schema={'a': pl.Categorical})
    #>           # Your operations go here.
    #>           pl.concat([df1, df2])
    #> 
    #>       Alternatively, if the performance cost is acceptable, you could just set:
    #> 
    #>           import polars as pl
    #>           pl.enable_string_cache()
    #> 
    #>       on startup.
    #> >
