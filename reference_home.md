
# Reference

`polars` provides a large number of functions for numerous data types
and this can sometimes be a bit overwhelming. Overall, you should be
able to do anything you want with `polars` by specifying the **data
structure** you want to use and then by applying **expressions** in a
particular **context**.

## Data structure

As explained in some vignettes, one of `polars` biggest strengths is the
ability to choose between eager and lazy evaluation, that require
respectively a `DataFrame` and a `LazyFrame` (with their counterparts
`GroupBy` and `LazyGroupBy` for grouped data).

We can apply functions directly on a `DataFrame` or `LazyFrame`, such as
`rename()` or `drop()`. Most functions that can be applied to
`DataFrame`s can also be used on `LazyFrame`s, but some are specific to
one or the other. For example:

- `$equals()` exists for `DataFrame` but not for `LazyFrame`;
- `$collect()` executes a lazy query, which means it can only be applied
  on a `LazyFrame`.

Another common data structure is the `Series`, which can be considered
as the equivalent of R vectors in `polars`’ world. Therefore, a
`DataFrame` is a list of `Series`.

Operations on `DataFrame` or `LazyFrame` are useful, but many more
operations can be applied on columns themselves by using various
**expressions** in different **contexts**.

## Contexts

A context simply is the type of data modification that is done. There
are 3 types of contexts:

- select and modify columns with `select()` and `with_columns()`;
- filter rows with `filter()`;
- group and aggregate rows with `group_by()` and `agg()`

Inside each context, you can use various **expressions** (aka. `Expr`).
Some expressions cannot be used in some contexts. For example, in
`with_columns()`, you can only apply expressions that return either the
same number of values or a single value that will be duplicated on all
rows:

``` r
test = pl$DataFrame(mtcars)
```

``` r
# this works
test$with_columns(
  pl$col("mpg") + 1
)
#> shape: (32, 11)
#> ┌──────┬─────┬───────┬───────┬───┬─────┬─────┬──────┬──────┐
#> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
#> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
#> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
#> ╞══════╪═════╪═══════╪═══════╪═══╪═════╪═════╪══════╪══════╡
#> │ 22.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
#> │ 22.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
#> │ 23.8 ┆ 4.0 ┆ 108.0 ┆ 93.0  ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 1.0  │
#> │ 22.4 ┆ 6.0 ┆ 258.0 ┆ 110.0 ┆ … ┆ 1.0 ┆ 0.0 ┆ 3.0  ┆ 1.0  │
#> │ 19.7 ┆ 8.0 ┆ 360.0 ┆ 175.0 ┆ … ┆ 0.0 ┆ 0.0 ┆ 3.0  ┆ 2.0  │
#> │ …    ┆ …   ┆ …     ┆ …     ┆ … ┆ …   ┆ …   ┆ …    ┆ …    │
#> │ 31.4 ┆ 4.0 ┆ 95.1  ┆ 113.0 ┆ … ┆ 1.0 ┆ 1.0 ┆ 5.0  ┆ 2.0  │
#> │ 16.8 ┆ 8.0 ┆ 351.0 ┆ 264.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 4.0  │
#> │ 20.7 ┆ 6.0 ┆ 145.0 ┆ 175.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 6.0  │
#> │ 16.0 ┆ 8.0 ┆ 301.0 ┆ 335.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 8.0  │
#> │ 22.4 ┆ 4.0 ┆ 121.0 ┆ 109.0 ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 2.0  │
#> └──────┴─────┴───────┴───────┴───┴─────┴─────┴──────┴──────┘
```

``` r
# this doesn't work because it returns only 2 values, while mtcars has 32 rows.
test$with_columns(
  pl$col("mpg")$slice(0, 2)
)
```

By contrast, in an `agg()` context, any number of return values are
possible, as they are returned in a list, and only the new columns or
the grouping columns are returned.

``` r
test$group_by(pl$col("cyl"))$agg(
  pl$col("mpg"), # varying number of values
  pl$col("mpg")$slice(0, 2)$name$suffix("_sliced"), # two values
  # aggregated to one value and implicitly unpacks list
  pl$col("mpg")$sum()$name$suffix("_summed")
)
#> shape: (3, 4)
#> ┌─────┬──────────────────────┬──────────────┬────────────┐
#> │ cyl ┆ mpg                  ┆ mpg_sliced   ┆ mpg_summed │
#> │ --- ┆ ---                  ┆ ---          ┆ ---        │
#> │ f64 ┆ list[f64]            ┆ list[f64]    ┆ f64        │
#> ╞═════╪══════════════════════╪══════════════╪════════════╡
#> │ 6.0 ┆ [21.0, 21.0, … 19.7] ┆ [21.0, 21.0] ┆ 138.2      │
#> │ 8.0 ┆ [18.7, 14.3, … 15.0] ┆ [18.7, 14.3] ┆ 211.4      │
#> │ 4.0 ┆ [22.8, 24.4, … 21.4] ┆ [22.8, 24.4] ┆ 293.3      │
#> └─────┴──────────────────────┴──────────────┴────────────┘
```

## Expressions

Expressions are the building blocks that give all the flexibility we
need to modify or create new columns.

Two important expressions starters are `pl$col()` (names a column in the
context) and `pl$lit()` (wraps a literal value or vector/series in an
Expr). Most other expression starters are syntactic sugar derived from
thereof, e.g. `pl$sum(_)` is actually `pl$col(_)$sum()`.

Expressions can be chained with more than 170 expression methods such as
`$sum()` which aggregates e.g. the column with summing.

``` r
# two examples of starting, chaining and combining expressions
pl$DataFrame(a = 1:4)$with_columns(
  # compute the cosine of column "a"
  a_cos = pl$col("a")$cos()$sin(),
  # standardize the values of column "a"
  a_stand = (pl$col("a") - pl$col("a")$mean()) / pl$col("a")$std(),
  # take 1:3, name it, then sum, then multiply by two
  lit_sum_add_two = pl$lit(1:3)$sum() * 2L
)
#> shape: (4, 4)
#> ┌─────┬───────────┬───────────┬─────────────────┐
#> │ a   ┆ a_cos     ┆ a_stand   ┆ lit_sum_add_two │
#> │ --- ┆ ---       ┆ ---       ┆ ---             │
#> │ i32 ┆ f64       ┆ f64       ┆ i32             │
#> ╞═════╪═══════════╪═══════════╪═════════════════╡
#> │ 1   ┆ 0.514395  ┆ -1.161895 ┆ 12              │
#> │ 2   ┆ -0.404239 ┆ -0.387298 ┆ 12              │
#> │ 3   ┆ -0.836022 ┆ 0.387298  ┆ 12              │
#> │ 4   ┆ -0.608083 ┆ 1.161895  ┆ 12              │
#> └─────┴───────────┴───────────┴─────────────────┘
```

Some methods share a common name but their behavior might be very
different depending on the input type. For example, `$decode()` doesn’t
do the same thing when it is applied on binary data or on string data.

To be able to distinguish those usages and to check the validity of a
query, `polars` stores methods in subnamespaces. For each datatype other
than numeric (floats and integers), there is a subnamespace containing
the available methods: `dt` (datetime), `list` (list), `str` (strings),
`struct` (structs), `cat` (categoricals) and `bin` (binary). As a
sidenote, there is also an exotic subnamespace called `meta` which is
rarely used to manipulate the expressions themselves. Each subsection in
the “Expressions” section lists all operations available for a specific
subnamespace.

For a concrete example for `dt`, suppose we have a column containing
dates and that we want to extract the year from these dates:

``` r
# Create the DataFrame
df = pl$DataFrame(
  date = pl$date_range(
    as.Date("2020-01-01"),
    as.Date("2023-01-02"),
    interval = "1y",
    eager = TRUE
  )
)
df
#> shape: (4, 1)
#> ┌────────────┐
#> │ date       │
#> │ ---        │
#> │ date       │
#> ╞════════════╡
#> │ 2020-01-01 │
#> │ 2021-01-01 │
#> │ 2022-01-01 │
#> │ 2023-01-01 │
#> └────────────┘
```

The function `year()` only makes sense for date-time data, so we look
for functions in the `dt` subnamespace (for **d**ate-**t**ime):

``` r
df$with_columns(
  year = pl$col("date")$dt$year()
)
#> shape: (4, 2)
#> ┌────────────┬──────┐
#> │ date       ┆ year │
#> │ ---        ┆ ---  │
#> │ date       ┆ i32  │
#> ╞════════════╪══════╡
#> │ 2020-01-01 ┆ 2020 │
#> │ 2021-01-01 ┆ 2021 │
#> │ 2022-01-01 ┆ 2022 │
#> │ 2023-01-01 ┆ 2023 │
#> └────────────┴──────┘
```

Similarly, to convert a string column to uppercase, we use the `str`
prefix before using `to_uppercase()`:

``` r
# Create the DataFrame
pl$DataFrame(foo = c("jake", "mary", "john peter"))$
  with_columns(upper = pl$col("foo")$str$to_uppercase())
#> shape: (3, 2)
#> ┌────────────┬────────────┐
#> │ foo        ┆ upper      │
#> │ ---        ┆ ---        │
#> │ str        ┆ str        │
#> ╞════════════╪════════════╡
#> │ jake       ┆ JAKE       │
#> │ mary       ┆ MARY       │
#> │ john peter ┆ JOHN PETER │
#> └────────────┴────────────┘
```
