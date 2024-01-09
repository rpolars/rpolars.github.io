
# To polars LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/as_polars.R#L190)

## Description

<code>as_polars_lf()</code> is a generic function that converts an R
object to a polars LazyFrame. It is basically a shortcut for
as_polars_df(x, …) with the $lazy() method.

## Usage

<pre><code class='language-R'>as_polars_lf(x, ...)

# Default S3 method:
as_polars_lf(x, ...)

# S3 method for class 'RPolarsLazyFrame'
as_polars_lf(x, ...)

# S3 method for class 'RPolarsLazyGroupBy'
as_polars_lf(x, ...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_lf_:_x">x</code>
</td>
<td>
Object to convert to a polars DataFrame.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_lf_:_...">…</code>
</td>
<td>
Additional arguments passed to methods.
</td>
</tr>
</table>

## Value

a LazyFrame

## Examples

``` r
library(polars)

as_polars_lf(mtcars)
```

    #> [1] "polars LazyFrame naive plan: (run ldf$describe_optimized_plan() to see the optimized plan)"
    #> DF ["mpg", "cyl", "disp", "hp"]; PROJECT */11 COLUMNS; SELECTION: "None"
