# Differences with Python Polars


We try to mimic the Python Polars API as much as possible so that one
can quickly switch and copy code between the two languages with as
little adjustments to make as possible (most of the time switching `.`
and `$` to chain methods).

Still, there are a few places where the API diverges. This is often due
to differences in the language itself. This vignette provides a list of
those differences.

## Converting data between Polars and R

### From R to Polars

The R package provides functions to create polars `DataFrame`,
`LazyFrame`, and `Series`. Like most of the functions, those are
designed to be close to their Python counterparts.

Still, R users are more used to `as.*` or `as_*` functions to convert
from or to other R objects. Therefore, in the documentation, we
sometimes prefer using `as_polars_df(<data>)` rather than
`pl$DataFrame(<data>)`.

### From Polars to R

While Python Polars has `to_pandas()`, we provide methods to convert
Polars data to standard R objects, such as `$to_list()` or
`$to_data_frame()`. However, the standard R user might find it more
familiar to call `as.data.frame()`, `as.list()` or `as.vector()` on
Polars structures.

## 64-bit integers

R doesn’t natively support 64-bit integers (Int64) but this is a
completely valid data type in Polars, which is based on the Arrow
specification. This means that handling Int64 values in `polars` objects
doesn’t deviate from the Python setting. However, we need to implement
some extra arguments when we want to pass data from Polars to R.

In particular, all functions that convert some polars data to R
(`as.data.frame()` and other methods such as `$to_list()`) have an
argument `int64_conversion` which specifies how Int64 values should be
handled. The default is to convert those Int64 to Float64, but it is
also possible to convert them to character or to keep them as Int64 by
using the package `bit64` under the hood.

This option can be set globally using
`options(polars.int64_conversion = "<value>")`. See `?polars_options()`
for more details.

## The `Object` data type

`Object` is a data type for wrapping arbitrary Python objects.
Therefore, it doesn’t have an equivalent in R.

When the user passes R objects with unsupported class to `polars`, it
will first try to convert them to a supported data type. For example, so
far the class `hms` from the eponymous package is not supported, so we
try to convert it to a numeric class:

``` r
hms::hms(56, 34, 12)
#> 12:34:56

pl$DataFrame(x = hms::hms(56, 34, 12))
#> shape: (1, 1)
#> ┌─────────┐
#> │ x       │
#> │ ---     │
#> │ f64     │
#> ╞═════════╡
#> │ 45296.0 │
#> └─────────┘
```

In some cases, there’s no conversion possible. For example, one cannot
convert a `geos` geometry to any supported data type. In this case, it
will raise an error:

``` r
geos::as_geos_geometry("LINESTRING (0 1, 3 9)")
#> <geos_geometry[1]>
#> [1] <LINESTRING (0 1, 3 9)>

pl$DataFrame(x = geos::as_geos_geometry("LINESTRING (0 1, 3 9)"))
#> Error: Execution halted with the following contexts
#>    0: In R: in $DataFrame():
#>    0: During function call [pl$DataFrame(x = geos::as_geos_geometry("LINESTRING (0 1, 3 9)"))]
#>    1: When constructing polars literal from Robj
#>    2: Encountered the following error in Rust-Polars:
#>         expected Series
```
