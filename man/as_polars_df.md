

# To polars DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/as_polars.R#L50)

## Description

<code>as_polars_df()</code> is a generic function that converts an R
object to a polars DataFrame. It is basically a wrapper for
pl$DataFrame(), but has special implementations for Apache Arrow-based
objects such as polars LazyFrame and arrow::Table.

## Usage

<pre><code class='language-R'>as_polars_df(x, ...)

# Default S3 method:
as_polars_df(x, ...)

# S3 method for class 'data.frame'
as_polars_df(x, ..., rownames = NULL, make_names_unique = TRUE)

# S3 method for class 'RPolarsDataFrame'
as_polars_df(x, ...)

# S3 method for class 'RPolarsGroupBy'
as_polars_df(x, ...)

# S3 method for class 'RPolarsRollingGroupBy'
as_polars_df(x, ...)

# S3 method for class 'RPolarsDynamicGroupBy'
as_polars_df(x, ...)

# S3 method for class 'RPolarsSeries'
as_polars_df(x, ...)

# S3 method for class 'RPolarsLazyFrame'
as_polars_df(
  x,
  n_rows = Inf,
  ...,
  type_coercion = TRUE,
  predicate_pushdown = TRUE,
  projection_pushdown = TRUE,
  simplify_expression = TRUE,
  slice_pushdown = TRUE,
  comm_subplan_elim = TRUE,
  comm_subexpr_elim = TRUE,
  streaming = FALSE,
  no_optimization = FALSE,
  inherit_optimization = FALSE,
  collect_in_background = FALSE
)

# S3 method for class 'RPolarsLazyGroupBy'
as_polars_df(x, ...)

# S3 method for class 'ArrowTabular'
as_polars_df(x, ..., rechunk = TRUE, schema = NULL, schema_overrides = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_df_:_x">x</code>
</td>
<td>
Object to convert to a polars DataFrame.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_df_:_...">…</code>
</td>
<td>
Additional arguments passed to methods.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_df_:_rownames">rownames</code>
</td>
<td>

How to treat existing row names of a data frame:

<ul>
<li>

<code>NULL</code>: Remove row names. This is the default.

</li>
<li>

A string: The name of a new column, which will contain the row names. If
<code>x</code> already has a column with that name, an error is thrown.

</li>
</ul>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_df_:_make_names_unique">make_names_unique</code>
</td>
<td>
A logical flag to replace duplicated column names with unique names. If
<code>FALSE</code> and there are duplicated column names, an error is
thrown.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_df_:_n_rows">n_rows</code>
</td>
<td>
Number of rows to fetch. Defaults to <code>Inf</code>, meaning all rows.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_df_:_type_coercion">type_coercion</code>
</td>
<td>
Boolean. Coerce types such that operations succeed and run on minimal
required memory.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_df_:_predicate_pushdown">predicate_pushdown</code>
</td>
<td>
Boolean. Applies filters as early as possible at scan level.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_df_:_projection_pushdown">projection_pushdown</code>
</td>
<td>
Boolean. Select only the columns that are needed at the scan level.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_df_:_simplify_expression">simplify_expression</code>
</td>
<td>
Boolean. Various optimizations, such as constant folding and replacing
expensive operations with faster alternatives.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_df_:_slice_pushdown">slice_pushdown</code>
</td>
<td>
Boolean. Only load the required slice from the scan level. Don’t
materialize sliced outputs (e.g. <code>join$head(10)</code>).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_df_:_comm_subplan_elim">comm_subplan_elim</code>
</td>
<td>
Boolean. Will try to cache branching subplans that occur on self-joins
or unions.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_df_:_comm_subexpr_elim">comm_subexpr_elim</code>
</td>
<td>
Boolean. Common subexpressions will be cached and reused.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_df_:_streaming">streaming</code>
</td>
<td>
Boolean. Run parts of the query in a streaming fashion (this is in an
alpha state).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_df_:_no_optimization">no_optimization</code>
</td>
<td>
Boolean. Sets the following parameters to <code>FALSE</code>:
<code>predicate_pushdown</code>, <code>projection_pushdown</code>,
<code>slice_pushdown</code>, <code>comm_subplan_elim</code>,
<code>comm_subexpr_elim</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_df_:_inherit_optimization">inherit_optimization</code>
</td>
<td>
Boolean. Use existing optimization settings regardless the settings
specified in this function call.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_df_:_collect_in_background">collect_in_background</code>
</td>
<td>
Boolean. Detach this query from R session. Computation will start in
background. Get a handle which later can be converted into the resulting
DataFrame. Useful in interactive mode to not lock R session.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_df_:_rechunk">rechunk</code>
</td>
<td>
A logical flag (default <code>TRUE</code>). Make sure that all data of
each column is in contiguous memory.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_df_:_schema">schema</code>
</td>
<td>
named list of DataTypes, or character vector of column names. Should be
the same length as the number of columns of <code>x</code>. If schema
names or types do not match <code>x</code>, the columns will be
renamed/recast. If <code>NULL</code> (default), convert columns as is.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="as_polars_df_:_schema_overrides">schema_overrides</code>
</td>
<td>
named list of DataTypes. Cast some columns to the DataType.
</td>
</tr>
</table>

## Details

For LazyFrame objects, this function is a shortcut for $collect() or
$fetch(), depending on whether the number of rows to fetch is infinite
or not.

## Value

a DataFrame

## Examples

``` r
library(polars)


# Convert the row names of a data frame to a column
as_polars_df(mtcars, rownames = "car")
```

    #> shape: (32, 12)
    #> ┌────────────────┬──────┬─────┬───────┬───┬─────┬─────┬──────┬──────┐
    #> │ car            ┆ mpg  ┆ cyl ┆ disp  ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
    #> │ ---            ┆ ---  ┆ --- ┆ ---   ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
    #> │ str            ┆ f64  ┆ f64 ┆ f64   ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
    #> ╞════════════════╪══════╪═════╪═══════╪═══╪═════╪═════╪══════╪══════╡
    #> │ Mazda RX4      ┆ 21.0 ┆ 6.0 ┆ 160.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
    #> │ Mazda RX4 Wag  ┆ 21.0 ┆ 6.0 ┆ 160.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
    #> │ Datsun 710     ┆ 22.8 ┆ 4.0 ┆ 108.0 ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 1.0  │
    #> │ Hornet 4 Drive ┆ 21.4 ┆ 6.0 ┆ 258.0 ┆ … ┆ 1.0 ┆ 0.0 ┆ 3.0  ┆ 1.0  │
    #> │ …              ┆ …    ┆ …   ┆ …     ┆ … ┆ …   ┆ …   ┆ …    ┆ …    │
    #> │ Ford Pantera L ┆ 15.8 ┆ 8.0 ┆ 351.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 4.0  │
    #> │ Ferrari Dino   ┆ 19.7 ┆ 6.0 ┆ 145.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 6.0  │
    #> │ Maserati Bora  ┆ 15.0 ┆ 8.0 ┆ 301.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 8.0  │
    #> │ Volvo 142E     ┆ 21.4 ┆ 4.0 ┆ 121.0 ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 2.0  │
    #> └────────────────┴──────┴─────┴───────┴───┴─────┴─────┴──────┴──────┘

``` r
# Convert an arrow Table to a polars DataFrame
at = arrow::arrow_table(x = 1:5, y = 6:10)
as_polars_df(at)
```

    #> shape: (5, 2)
    #> ┌─────┬─────┐
    #> │ x   ┆ y   │
    #> │ --- ┆ --- │
    #> │ i32 ┆ i32 │
    #> ╞═════╪═════╡
    #> │ 1   ┆ 6   │
    #> │ 2   ┆ 7   │
    #> │ 3   ┆ 8   │
    #> │ 4   ┆ 9   │
    #> │ 5   ┆ 10  │
    #> └─────┴─────┘

``` r
# Convert an arrow Table, with renaming all columns
as_polars_df(
  at,
  schema = c("a", "b")
)
```

    #> shape: (5, 2)
    #> ┌─────┬─────┐
    #> │ a   ┆ b   │
    #> │ --- ┆ --- │
    #> │ i32 ┆ i32 │
    #> ╞═════╪═════╡
    #> │ 1   ┆ 6   │
    #> │ 2   ┆ 7   │
    #> │ 3   ┆ 8   │
    #> │ 4   ┆ 9   │
    #> │ 5   ┆ 10  │
    #> └─────┴─────┘

``` r
# Convert an arrow Table, with renaming and casting all columns
as_polars_df(
  at,
  schema = list(a = pl$Int64, b = pl$String)
)
```

    #> shape: (5, 2)
    #> ┌─────┬─────┐
    #> │ a   ┆ b   │
    #> │ --- ┆ --- │
    #> │ i64 ┆ str │
    #> ╞═════╪═════╡
    #> │ 1   ┆ 6   │
    #> │ 2   ┆ 7   │
    #> │ 3   ┆ 8   │
    #> │ 4   ┆ 9   │
    #> │ 5   ┆ 10  │
    #> └─────┴─────┘

``` r
# Convert an arrow Table, with renaming and casting some columns
as_polars_df(
  at,
  schema_overrides = list(y = pl$String) # cast some columns
)
```

    #> shape: (5, 2)
    #> ┌─────┬─────┐
    #> │ x   ┆ y   │
    #> │ --- ┆ --- │
    #> │ i32 ┆ str │
    #> ╞═════╪═════╡
    #> │ 1   ┆ 6   │
    #> │ 2   ┆ 7   │
    #> │ 3   ┆ 8   │
    #> │ 4   ┆ 9   │
    #> │ 5   ┆ 10  │
    #> └─────┴─────┘

``` r
# Create a polars DataFrame from a data.frame
lf = as_polars_df(mtcars)$lazy()

# Collect all rows from the LazyFrame
as_polars_df(lf)
```

    #> shape: (32, 11)
    #> ┌──────┬─────┬───────┬───────┬───┬─────┬─────┬──────┬──────┐
    #> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
    #> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
    #> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
    #> ╞══════╪═════╪═══════╪═══════╪═══╪═════╪═════╪══════╪══════╡
    #> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
    #> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
    #> │ 22.8 ┆ 4.0 ┆ 108.0 ┆ 93.0  ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 1.0  │
    #> │ 21.4 ┆ 6.0 ┆ 258.0 ┆ 110.0 ┆ … ┆ 1.0 ┆ 0.0 ┆ 3.0  ┆ 1.0  │
    #> │ …    ┆ …   ┆ …     ┆ …     ┆ … ┆ …   ┆ …   ┆ …    ┆ …    │
    #> │ 15.8 ┆ 8.0 ┆ 351.0 ┆ 264.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 4.0  │
    #> │ 19.7 ┆ 6.0 ┆ 145.0 ┆ 175.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 6.0  │
    #> │ 15.0 ┆ 8.0 ┆ 301.0 ┆ 335.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 8.0  │
    #> │ 21.4 ┆ 4.0 ┆ 121.0 ┆ 109.0 ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 2.0  │
    #> └──────┴─────┴───────┴───────┴───┴─────┴─────┴──────┴──────┘

``` r
# Fetch 5 rows from the LazyFrame
as_polars_df(lf, 5)
```

    #> shape: (5, 11)
    #> ┌──────┬─────┬───────┬───────┬───┬─────┬─────┬──────┬──────┐
    #> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
    #> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
    #> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
    #> ╞══════╪═════╪═══════╪═══════╪═══╪═════╪═════╪══════╪══════╡
    #> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
    #> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
    #> │ 22.8 ┆ 4.0 ┆ 108.0 ┆ 93.0  ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 1.0  │
    #> │ 21.4 ┆ 6.0 ┆ 258.0 ┆ 110.0 ┆ … ┆ 1.0 ┆ 0.0 ┆ 3.0  ┆ 1.0  │
    #> │ 18.7 ┆ 8.0 ┆ 360.0 ┆ 175.0 ┆ … ┆ 0.0 ┆ 0.0 ┆ 3.0  ┆ 2.0  │
    #> └──────┴─────┴───────┴───────┴───┴─────┴─────┴──────┴──────┘
