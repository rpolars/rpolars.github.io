# An Introduction to Polars from R


## What is Polars?

Polars is [a lightning fast](https://duckdblabs.github.io/db-benchmark/)
Data Frame library. Its embarrassingly parallel execution, cache
efficient algorithms and expressive API makes it perfect for efficient
data wrangling, data pipelines, snappy APIs, and much more besides.
Polars also supports “streaming mode” for out-of-memory operations. This
allows users to analyze datasets many times larger than RAM.

The underlying computation engine is written in Rust and is built on the
Apache Arrow columnar memory format. It can be used in Rust or via
Python bindings. The **polars** R-package provides equivalent bindings
from R. To help distinguish the different language implementations, we
typically use a convention of referring to them with prefixes:
rust-polars, py-polars, r-polars, nodejs-polars, etc. But within each
language, the relevant library is always just called *polars*.

**polars** users can expect orders of magnitude(s) improvement compared
to **dplyr** for simple transformations on datasets \>500Mb. The
automatic Polars optimization framework means that that this speed boost
can be even greater for complex queries that chain together many
operations. Performance is similar to that of **data.table**, although
**polars** supports additional functionality via its relationship to the
Apache Arrow memory model. For example, it can scan multiple Parquet
files and datasets and selectively import random subsets without having
to read all of the data.

Polars syntax is similar to that of Spark, but the workflow is
column-oriented rather than row-oriented. Since R is itself a
column-oriented language, this should immediately feel familiar to most
R users. Like Spark and modern SQL variants, Polars optimizes queries
for memory consumption and speed, so you don’t have to. However, unlike
Spark, Polars is natively multithreaded instead of multinoded. This
makes (r)polars much simpler to install and can be used as one would any
other R package.

This R port relies on the excellent
[**extendr**](https://github.com/extendr) package, which is the R
equivalent to pyo3+maturin. **extendr** is very convenient for calling
Rust from R, and vice versa, and is what we use to build the **polars**
package. Once built, however, **polars** has no other dependencies other
than R itself. This makes it very fast and lightweight to install, and
so **polars** can immediately be used to tackle your big (or small!)
data wrangling tasks.

## Documentation and tutorials

Users can find detailed documentation for all objects, functions, and
methods on the Reference page of [this
website](https://rpolars.github.io/). This documentation can also be
accessed from the R console using the typical `?` syntax. For example,
we will later use the `DataFrame()` constructor function and apply the
`group_by()` method to a `DataFrame` object. The documentation for these
can be accessed by typing these commands:

``` r
?DataFrame_class
?DataFrame_group_by
```

The [Polars book](https://pola-rs.github.io/polars-book/user-guide/)
offers a great introduction to the Polars data frame library, with a
very large number of examples in Python and Rust. The syntax and
expressions in the `polars` package for R are (deliberately) as close to
the Python implementation as possible, so you can always refer to the
[polars book](https://pola-rs.github.io/polars-book/user-guide/) for
more ideas. Just remember to switch out any “.” (Python) for a “$” (R)
when chaining methods. For example, here are two equivalent lines of
code for some hypothetical dataset.

``` python
# Python
df.group_by("id").mean()
```

``` r
# R
df$group_by("id")$mean()
```

## `Series` and `DataFrames`

In `polars`, objects of class `Series` are analogous to R vectors.
Objects of class `DataFrame` are analogous to R data frames. Notice that
to avoid collision with classes provided by other packages, the class
name of all objects created by `polars` starts with “RPolars”. For
example, a `polars` `DataFrame` has the class “RPolarsDataFrame”.

To create Polars `Series` and `DataFrames` objects, we load the library
and use constructor functions with the `pl$` prefix. This prefix is very
important, as most of the `polars` functions are made available via
`pl$`:

``` r
library(polars)

pl$Series((1:5) * 5)
#> polars Series: shape: (5,)
#> Series: '' [f64]
#> [
#>  5.0
#>  10.0
#>  15.0
#>  20.0
#>  25.0
#> ]

pl$DataFrame(a = 1:5, b = letters[1:5])
#> shape: (5, 2)
#> ┌─────┬─────┐
#> │ a   ┆ b   │
#> │ --- ┆ --- │
#> │ i32 ┆ str │
#> ╞═════╪═════╡
#> │ 1   ┆ a   │
#> │ 2   ┆ b   │
#> │ 3   ┆ c   │
#> │ 4   ┆ d   │
#> │ 5   ┆ e   │
#> └─────┴─────┘
```

Or, to convert existing R objects to Polars objects, we can use the
`as_polars_series()` and `as_polars_df()` generic functions.

``` r
ser = as_polars_series((1:5) * 5)
ser
#> polars Series: shape: (5,)
#> Series: '' [f64]
#> [
#>  5.0
#>  10.0
#>  15.0
#>  20.0
#>  25.0
#> ]

dat = as_polars_df(mtcars)
dat
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
#> │ 18.7 ┆ 8.0 ┆ 360.0 ┆ 175.0 ┆ … ┆ 0.0 ┆ 0.0 ┆ 3.0  ┆ 2.0  │
#> │ …    ┆ …   ┆ …     ┆ …     ┆ … ┆ …   ┆ …   ┆ …    ┆ …    │
#> │ 30.4 ┆ 4.0 ┆ 95.1  ┆ 113.0 ┆ … ┆ 1.0 ┆ 1.0 ┆ 5.0  ┆ 2.0  │
#> │ 15.8 ┆ 8.0 ┆ 351.0 ┆ 264.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 4.0  │
#> │ 19.7 ┆ 6.0 ┆ 145.0 ┆ 175.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 6.0  │
#> │ 15.0 ┆ 8.0 ┆ 301.0 ┆ 335.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 8.0  │
#> │ 21.4 ┆ 4.0 ┆ 121.0 ┆ 109.0 ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 2.0  │
#> └──────┴─────┴───────┴───────┴───┴─────┴─────┴──────┴──────┘
```

`pl$DataFrame()` is similar to `data.frame()`, and `as_polars_df()` is
similar to `as.data.frame()`.

Both Polars and R are column-orientated. So you can think of
`DataFrames` (data.frames) as being made up of a collection of `Series`
(vectors). In fact, you can create a new Polars `DataFrame` as a mix of
`Series` and/or regular R vectors.

``` r
pl$DataFrame(
  a = pl$Series((1:5) * 5),
  b = pl$Series(letters[1:5]),
  c = pl$Series(c(1, 2, 3, 4, 5)),
  d = c(15, 14, 13, 12, 11),
  c(5, 4, 3, 2, 1),
  1:5
)
#> shape: (5, 6)
#> ┌──────┬─────┬─────┬──────┬────────────┬──────────────┐
#> │ a    ┆ b   ┆ c   ┆ d    ┆ new_column ┆ new_column_1 │
#> │ ---  ┆ --- ┆ --- ┆ ---  ┆ ---        ┆ ---          │
#> │ f64  ┆ str ┆ f64 ┆ f64  ┆ f64        ┆ i32          │
#> ╞══════╪═════╪═════╪══════╪════════════╪══════════════╡
#> │ 5.0  ┆ a   ┆ 1.0 ┆ 15.0 ┆ 5.0        ┆ 1            │
#> │ 10.0 ┆ b   ┆ 2.0 ┆ 14.0 ┆ 4.0        ┆ 2            │
#> │ 15.0 ┆ c   ┆ 3.0 ┆ 13.0 ┆ 3.0        ┆ 3            │
#> │ 20.0 ┆ d   ┆ 4.0 ┆ 12.0 ┆ 2.0        ┆ 4            │
#> │ 25.0 ┆ e   ┆ 5.0 ┆ 11.0 ┆ 1.0        ┆ 5            │
#> └──────┴─────┴─────┴──────┴────────────┴──────────────┘
```

`Series` and `DataFrame` can be operated on using many standard R
functions. For example:

``` r
# Series
length(ser)
#> [1] 5

max(ser)
#> [1] 25

# DataFrame
dat[c(1:3, 12), c("mpg", "hp")]
#> shape: (4, 2)
#> ┌──────┬───────┐
#> │ mpg  ┆ hp    │
#> │ ---  ┆ ---   │
#> │ f64  ┆ f64   │
#> ╞══════╪═══════╡
#> │ 21.0 ┆ 110.0 │
#> │ 21.0 ┆ 110.0 │
#> │ 22.8 ┆ 93.0  │
#> │ 16.4 ┆ 180.0 │
#> └──────┴───────┘

names(dat)
#>  [1] "mpg"  "cyl"  "disp" "hp"   "drat" "wt"   "qsec" "vs"   "am"   "gear"
#> [11] "carb"

dim(dat)
#> [1] 32 11

head(dat, n = 2)
#> shape: (2, 11)
#> ┌──────┬─────┬───────┬───────┬───┬─────┬─────┬──────┬──────┐
#> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
#> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
#> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
#> ╞══════╪═════╪═══════╪═══════╪═══╪═════╪═════╪══════╪══════╡
#> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
#> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
#> └──────┴─────┴───────┴───────┴───┴─────┴─────┴──────┴──────┘
```

## Methods and pipelines

Although some simple R functions work out of the box on **polars**
objects, the full power of Polars is realized via *methods*. Polars
methods are accessed using the `$` syntax. For example, to sort a
`Series` object, we use the `$sort()` method:

``` r
ser$sort()
#> polars Series: shape: (5,)
#> Series: '' [f64]
#> [
#>  5.0
#>  10.0
#>  15.0
#>  20.0
#>  25.0
#> ]
```

There are numerous methods designed to accomplish various tasks:

``` r
ser$max()
#> [1] 25

dat$slice(offset = 2, length = 3)
#> shape: (3, 11)
#> ┌──────┬─────┬───────┬───────┬───┬─────┬─────┬──────┬──────┐
#> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
#> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
#> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
#> ╞══════╪═════╪═══════╪═══════╪═══╪═════╪═════╪══════╪══════╡
#> │ 22.8 ┆ 4.0 ┆ 108.0 ┆ 93.0  ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 1.0  │
#> │ 21.4 ┆ 6.0 ┆ 258.0 ┆ 110.0 ┆ … ┆ 1.0 ┆ 0.0 ┆ 3.0  ┆ 1.0  │
#> │ 18.7 ┆ 8.0 ┆ 360.0 ┆ 175.0 ┆ … ┆ 0.0 ┆ 0.0 ┆ 3.0  ┆ 2.0  │
#> └──────┴─────┴───────┴───────┴───┴─────┴─────┴──────┴──────┘
```

One advantage of using methods is that many more operations are possible
on Polars objects using methods than through base R functions.

A second advantage is *Methods Chaining*, a core part of the Polars
workflow. If you are coming from one of the other popular data wrangling
libraries in R, then you probably already have an innate sense of what
this means. For instance,

-   In **dplyr** we use a pipe operator,
    e.g. `dat |> filter(...) |> select(...)`
-   In **data.table** we use its indexing syntax,
    e.g. `DT[i, j, by][...]`
-   Etc.

In **polars** our method chaining syntax takes the form
`object$m1()$m2()`, where `object` is our data object, and `m1()` and
`m2()` are appropriate methods, like subsetting or aggregation
expressions.

This might all seem a little abstract, so let’s walk through some quick
examples to help make things concrete. We continue with the `mtcars`
dataset that we coerced to a `DataFrame` in the introduction.[1]

To start, say we compute the maximum value in each column. We can use
the `max()` method:

``` r
dat$max()
#> shape: (1, 11)
#> ┌──────┬─────┬───────┬───────┬───┬─────┬─────┬──────┬──────┐
#> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
#> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
#> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
#> ╞══════╪═════╪═══════╪═══════╪═══╪═════╪═════╪══════╪══════╡
#> │ 33.9 ┆ 8.0 ┆ 472.0 ┆ 335.0 ┆ … ┆ 1.0 ┆ 1.0 ┆ 5.0  ┆ 8.0  │
#> └──────┴─────┴───────┴───────┴───┴─────┴─────┴──────┴──────┘
```

Now, we first use the `$tail` method to select the last 10 rows of the
dataset, and then use the `$max` method to compute the maximums in those
10 rows:

``` r
dat$tail(10)$max()
#> shape: (1, 11)
#> ┌──────┬─────┬───────┬───────┬───┬─────┬─────┬──────┬──────┐
#> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
#> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
#> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
#> ╞══════╪═════╪═══════╪═══════╪═══╪═════╪═════╪══════╪══════╡
#> │ 30.4 ┆ 8.0 ┆ 400.0 ┆ 335.0 ┆ … ┆ 1.0 ┆ 1.0 ┆ 5.0  ┆ 8.0  │
#> └──────┴─────┴───────┴───────┴───┴─────┴─────┴──────┴──────┘
```

Finally, we convert the result to a standard R data frame:

``` r
dat$tail(10)$max() |>
  as.data.frame()
#>    mpg cyl disp  hp drat    wt qsec vs am gear carb
#> 1 30.4   8  400 335 4.43 3.845 18.9  1  1    5    8
```

Below, we will introduce several other methods, including `$select`,
`$filter`, and `$group_by` which allow us to do powerful data
manipulations easily. To give you a small taste, we now take group-wise
means:

``` r
dat$group_by("cyl")$mean()
#> shape: (3, 11)
#> ┌─────┬───────────┬────────────┬────────────┬───┬──────────┬──────────┬──────────┬──────────┐
#> │ cyl ┆ mpg       ┆ disp       ┆ hp         ┆ … ┆ vs       ┆ am       ┆ gear     ┆ carb     │
#> │ --- ┆ ---       ┆ ---        ┆ ---        ┆   ┆ ---      ┆ ---      ┆ ---      ┆ ---      │
#> │ f64 ┆ f64       ┆ f64        ┆ f64        ┆   ┆ f64      ┆ f64      ┆ f64      ┆ f64      │
#> ╞═════╪═══════════╪════════════╪════════════╪═══╪══════════╪══════════╪══════════╪══════════╡
#> │ 4.0 ┆ 26.663636 ┆ 105.136364 ┆ 82.636364  ┆ … ┆ 0.909091 ┆ 0.727273 ┆ 4.090909 ┆ 1.545455 │
#> │ 8.0 ┆ 15.1      ┆ 353.1      ┆ 209.214286 ┆ … ┆ 0.0      ┆ 0.142857 ┆ 3.285714 ┆ 3.5      │
#> │ 6.0 ┆ 19.742857 ┆ 183.314286 ┆ 122.285714 ┆ … ┆ 0.571429 ┆ 0.428571 ┆ 3.857143 ┆ 3.428571 │
#> └─────┴───────────┴────────────┴────────────┴───┴──────────┴──────────┴──────────┴──────────┘
```

## Subset

We can now start chaining together various methods (expressions) to
manipulate it in different ways. For example, we can subset the data by
rows ([`filter()`](https://rpolars.github.io/man/DataFrame_filter.html))
and also columns
([`select()`](https://rpolars.github.io/man/DataFrame_select.html)):

``` r
dat$filter(pl$col("cyl") == 6)
#> shape: (7, 11)
#> ┌──────┬─────┬───────┬───────┬───┬─────┬─────┬──────┬──────┐
#> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
#> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
#> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
#> ╞══════╪═════╪═══════╪═══════╪═══╪═════╪═════╪══════╪══════╡
#> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
#> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
#> │ 21.4 ┆ 6.0 ┆ 258.0 ┆ 110.0 ┆ … ┆ 1.0 ┆ 0.0 ┆ 3.0  ┆ 1.0  │
#> │ 18.1 ┆ 6.0 ┆ 225.0 ┆ 105.0 ┆ … ┆ 1.0 ┆ 0.0 ┆ 3.0  ┆ 1.0  │
#> │ 19.2 ┆ 6.0 ┆ 167.6 ┆ 123.0 ┆ … ┆ 1.0 ┆ 0.0 ┆ 4.0  ┆ 4.0  │
#> │ 17.8 ┆ 6.0 ┆ 167.6 ┆ 123.0 ┆ … ┆ 1.0 ┆ 0.0 ┆ 4.0  ┆ 4.0  │
#> │ 19.7 ┆ 6.0 ┆ 145.0 ┆ 175.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 6.0  │
#> └──────┴─────┴───────┴───────┴───┴─────┴─────┴──────┴──────┘

dat$filter(pl$col("cyl") == 6 & pl$col("am") == 1)
#> shape: (3, 11)
#> ┌──────┬─────┬───────┬───────┬───┬─────┬─────┬──────┬──────┐
#> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
#> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
#> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
#> ╞══════╪═════╪═══════╪═══════╪═══╪═════╪═════╪══════╪══════╡
#> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
#> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
#> │ 19.7 ┆ 6.0 ┆ 145.0 ┆ 175.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 6.0  │
#> └──────┴─────┴───────┴───────┴───┴─────┴─────┴──────┴──────┘

dat$select(pl$col(c("mpg", "hp")))
#> shape: (32, 2)
#> ┌──────┬───────┐
#> │ mpg  ┆ hp    │
#> │ ---  ┆ ---   │
#> │ f64  ┆ f64   │
#> ╞══════╪═══════╡
#> │ 21.0 ┆ 110.0 │
#> │ 21.0 ┆ 110.0 │
#> │ 22.8 ┆ 93.0  │
#> │ 21.4 ┆ 110.0 │
#> │ 18.7 ┆ 175.0 │
#> │ …    ┆ …     │
#> │ 30.4 ┆ 113.0 │
#> │ 15.8 ┆ 264.0 │
#> │ 19.7 ┆ 175.0 │
#> │ 15.0 ┆ 335.0 │
#> │ 21.4 ┆ 109.0 │
#> └──────┴───────┘
```

Of course, we can chain those methods to create a pipeline:

``` r
dat$filter(
  pl$col("cyl") == 6
)$select(
  pl$col(c("mpg", "hp", "cyl"))
)
#> shape: (7, 3)
#> ┌──────┬───────┬─────┐
#> │ mpg  ┆ hp    ┆ cyl │
#> │ ---  ┆ ---   ┆ --- │
#> │ f64  ┆ f64   ┆ f64 │
#> ╞══════╪═══════╪═════╡
#> │ 21.0 ┆ 110.0 ┆ 6.0 │
#> │ 21.0 ┆ 110.0 ┆ 6.0 │
#> │ 21.4 ┆ 110.0 ┆ 6.0 │
#> │ 18.1 ┆ 105.0 ┆ 6.0 │
#> │ 19.2 ┆ 123.0 ┆ 6.0 │
#> │ 17.8 ┆ 123.0 ┆ 6.0 │
#> │ 19.7 ┆ 175.0 ┆ 6.0 │
#> └──────┴───────┴─────┘
```

## Aggregate and modify

The `select()` method that we introduced above also supports data
modification, so you can simultaneously transform it while you are
subsetting. However, the result will exclude any columns that weren’t
specified as part of the expression. To modify or add some
columns—whilst preserving all others in the dataset—it is therefore
better to use the
[`with_columns()`](https://rpolars.github.io/man/DataFrame_with_columns.html)
method. This next code chunk is equivalent to
`mtcars |> dplyr::mutate(sum_mpg=sum(mpg), sum_hp=sum(hp), .by = cyl)`.

``` r
# Add the grouped sums of some selected columns.
dat$with_columns(
  pl$col("mpg")$sum()$over("cyl")$alias("sum_mpg"),
  pl$col("hp")$sum()$over("cyl")$alias("sum_hp")
)
#> shape: (32, 13)
#> ┌──────┬─────┬───────┬───────┬───┬──────┬──────┬─────────┬────────┐
#> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ gear ┆ carb ┆ sum_mpg ┆ sum_hp │
#> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ ---  ┆ ---  ┆ ---     ┆ ---    │
#> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64  ┆ f64  ┆ f64     ┆ f64    │
#> ╞══════╪═════╪═══════╪═══════╪═══╪══════╪══════╪═════════╪════════╡
#> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 4.0  ┆ 4.0  ┆ 138.2   ┆ 856.0  │
#> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 4.0  ┆ 4.0  ┆ 138.2   ┆ 856.0  │
#> │ 22.8 ┆ 4.0 ┆ 108.0 ┆ 93.0  ┆ … ┆ 4.0  ┆ 1.0  ┆ 293.3   ┆ 909.0  │
#> │ 21.4 ┆ 6.0 ┆ 258.0 ┆ 110.0 ┆ … ┆ 3.0  ┆ 1.0  ┆ 138.2   ┆ 856.0  │
#> │ 18.7 ┆ 8.0 ┆ 360.0 ┆ 175.0 ┆ … ┆ 3.0  ┆ 2.0  ┆ 211.4   ┆ 2929.0 │
#> │ …    ┆ …   ┆ …     ┆ …     ┆ … ┆ …    ┆ …    ┆ …       ┆ …      │
#> │ 30.4 ┆ 4.0 ┆ 95.1  ┆ 113.0 ┆ … ┆ 5.0  ┆ 2.0  ┆ 293.3   ┆ 909.0  │
#> │ 15.8 ┆ 8.0 ┆ 351.0 ┆ 264.0 ┆ … ┆ 5.0  ┆ 4.0  ┆ 211.4   ┆ 2929.0 │
#> │ 19.7 ┆ 6.0 ┆ 145.0 ┆ 175.0 ┆ … ┆ 5.0  ┆ 6.0  ┆ 138.2   ┆ 856.0  │
#> │ 15.0 ┆ 8.0 ┆ 301.0 ┆ 335.0 ┆ … ┆ 5.0  ┆ 8.0  ┆ 211.4   ┆ 2929.0 │
#> │ 21.4 ┆ 4.0 ┆ 121.0 ┆ 109.0 ┆ … ┆ 4.0  ┆ 2.0  ┆ 293.3   ┆ 909.0  │
#> └──────┴─────┴───────┴───────┴───┴──────┴──────┴─────────┴────────┘
```

For what it’s worth, the previous query could have been written more
concisely as:

``` r
dat$with_columns(
  pl$col(c("mpg", "hp"))$sum()$over("cyl")$name$prefix("sum_")
)
#> shape: (32, 13)
#> ┌──────┬─────┬───────┬───────┬───┬──────┬──────┬─────────┬────────┐
#> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ gear ┆ carb ┆ sum_mpg ┆ sum_hp │
#> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ ---  ┆ ---  ┆ ---     ┆ ---    │
#> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64  ┆ f64  ┆ f64     ┆ f64    │
#> ╞══════╪═════╪═══════╪═══════╪═══╪══════╪══════╪═════════╪════════╡
#> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 4.0  ┆ 4.0  ┆ 138.2   ┆ 856.0  │
#> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 4.0  ┆ 4.0  ┆ 138.2   ┆ 856.0  │
#> │ 22.8 ┆ 4.0 ┆ 108.0 ┆ 93.0  ┆ … ┆ 4.0  ┆ 1.0  ┆ 293.3   ┆ 909.0  │
#> │ 21.4 ┆ 6.0 ┆ 258.0 ┆ 110.0 ┆ … ┆ 3.0  ┆ 1.0  ┆ 138.2   ┆ 856.0  │
#> │ 18.7 ┆ 8.0 ┆ 360.0 ┆ 175.0 ┆ … ┆ 3.0  ┆ 2.0  ┆ 211.4   ┆ 2929.0 │
#> │ …    ┆ …   ┆ …     ┆ …     ┆ … ┆ …    ┆ …    ┆ …       ┆ …      │
#> │ 30.4 ┆ 4.0 ┆ 95.1  ┆ 113.0 ┆ … ┆ 5.0  ┆ 2.0  ┆ 293.3   ┆ 909.0  │
#> │ 15.8 ┆ 8.0 ┆ 351.0 ┆ 264.0 ┆ … ┆ 5.0  ┆ 4.0  ┆ 211.4   ┆ 2929.0 │
#> │ 19.7 ┆ 6.0 ┆ 145.0 ┆ 175.0 ┆ … ┆ 5.0  ┆ 6.0  ┆ 138.2   ┆ 856.0  │
#> │ 15.0 ┆ 8.0 ┆ 301.0 ┆ 335.0 ┆ … ┆ 5.0  ┆ 8.0  ┆ 211.4   ┆ 2929.0 │
#> │ 21.4 ┆ 4.0 ┆ 121.0 ┆ 109.0 ┆ … ┆ 4.0  ┆ 2.0  ┆ 293.3   ┆ 909.0  │
#> └──────┴─────┴───────┴───────┴───┴──────┴──────┴─────────┴────────┘
```

Similarly, here’s how we could have aggregated (i.e., collapsed) the
dataset by groups instead of modifying them. We need simply invoke the
`group_by()` and
[`agg()`](https://rpolars.github.io/man/Expr_agg_groups.html) methods.

``` r
dat$group_by(
  "cyl",
  maintain_order = TRUE
)$agg(
  pl$col(c("mpg", "hp"))$sum()
)
#> shape: (3, 3)
#> ┌─────┬───────┬────────┐
#> │ cyl ┆ mpg   ┆ hp     │
#> │ --- ┆ ---   ┆ ---    │
#> │ f64 ┆ f64   ┆ f64    │
#> ╞═════╪═══════╪════════╡
#> │ 6.0 ┆ 138.2 ┆ 856.0  │
#> │ 4.0 ┆ 293.3 ┆ 909.0  │
#> │ 8.0 ┆ 211.4 ┆ 2929.0 │
#> └─────┴───────┴────────┘
```

(arg `maintain_order = TRUE` is optional, since **polars** doesn’t sort
the results of grouped operations by default. This is similar to what
**data.table** does and is also true for newer versions of **dplyr**.)

The same principles of method chaining can be combined very flexibly to
group by multiple variables and aggregation types.

``` r
dat$group_by(
  "cyl",
  pl$col("am")$cast(pl$Boolean)$alias("manual")
)$agg(
  pl$col("mpg")$mean()$alias("mean_mpg"),
  pl$col("hp")$median()$alias("med_hp")
)
#> shape: (6, 4)
#> ┌─────┬────────┬───────────┬────────┐
#> │ cyl ┆ manual ┆ mean_mpg  ┆ med_hp │
#> │ --- ┆ ---    ┆ ---       ┆ ---    │
#> │ f64 ┆ bool   ┆ f64       ┆ f64    │
#> ╞═════╪════════╪═══════════╪════════╡
#> │ 6.0 ┆ true   ┆ 20.566667 ┆ 110.0  │
#> │ 8.0 ┆ false  ┆ 15.05     ┆ 180.0  │
#> │ 4.0 ┆ true   ┆ 28.075    ┆ 78.5   │
#> │ 6.0 ┆ false  ┆ 19.125    ┆ 116.5  │
#> │ 4.0 ┆ false  ┆ 22.9      ┆ 95.0   │
#> │ 8.0 ┆ true   ┆ 15.4      ┆ 299.5  │
#> └─────┴────────┴───────────┴────────┘
```

Note that we used the `cast` method to convert the data type of the `am`
column. See the section below for more details on data types.

## Reshape

Polars supports data reshaping, going from both long to wide (“pivot”)
and wide to long (“melt”). Let’s switch to the `Indometh` dataset to
demonstrate some basic examples. Note that the data are currently in
long format.

``` r
indo = as_polars_df(Indometh)
```

To go from long to wide, we use the `pivot` method. Here we pivot the
data so that every subject takes its own column.

``` r
indo_wide = indo$pivot(values = "conc", index = "time", columns = "Subject")
```

To go from wide to long, we use the `melt` method.

``` r
# indo_wide$melt(id_vars = "time") # default column names are "variable" and "value"
indo_wide$melt(id_vars = "time", variable_name = "subject", value_name = "conc")
#> shape: (66, 3)
#> ┌──────┬─────────┬──────┐
#> │ time ┆ subject ┆ conc │
#> │ ---  ┆ ---     ┆ ---  │
#> │ f64  ┆ str     ┆ f64  │
#> ╞══════╪═════════╪══════╡
#> │ 0.25 ┆ 1       ┆ 1.5  │
#> │ 0.5  ┆ 1       ┆ 0.94 │
#> │ 0.75 ┆ 1       ┆ 0.78 │
#> │ 1.0  ┆ 1       ┆ 0.48 │
#> │ 1.25 ┆ 1       ┆ 0.37 │
#> │ …    ┆ …       ┆ …    │
#> │ 3.0  ┆ 6       ┆ 0.24 │
#> │ 4.0  ┆ 6       ┆ 0.17 │
#> │ 5.0  ┆ 6       ┆ 0.13 │
#> │ 6.0  ┆ 6       ┆ 0.1  │
#> │ 8.0  ┆ 6       ┆ 0.09 │
#> └──────┴─────────┴──────┘
```

Basic functionality aside, it should be noted that `pivot` can perform
aggregations as part of the reshaping operation. This is useful when you
have multiple observations per ID variable that need to be collapsed
into unique values. The aggregating functions can be arbitrarily
complex, but let’s consider a relatively simple example using our `dat`
(“mtcars”) DataFrame from earlier: what is the median MPG value (`mpg`)
across cylinders (`cyl`), cut by different combinations of transmission
type (`am`) and engine shape (`vs`)?

``` r
dat$pivot(
  values = "mpg",
  index = c("am", "vs"),
  columns = "cyl",
  aggregate_fun = "median" # aggregating function
)
#> shape: (4, 5)
#> ┌─────┬─────┬───────┬──────┬──────┐
#> │ am  ┆ vs  ┆ 6.0   ┆ 4.0  ┆ 8.0  │
#> │ --- ┆ --- ┆ ---   ┆ ---  ┆ ---  │
#> │ f64 ┆ f64 ┆ f64   ┆ f64  ┆ f64  │
#> ╞═════╪═════╪═══════╪══════╪══════╡
#> │ 1.0 ┆ 0.0 ┆ 21.0  ┆ 26.0 ┆ 15.4 │
#> │ 1.0 ┆ 1.0 ┆ null  ┆ 30.4 ┆ null │
#> │ 0.0 ┆ 1.0 ┆ 18.65 ┆ 22.8 ┆ null │
#> │ 0.0 ┆ 0.0 ┆ null  ┆ null ┆ 15.2 │
#> └─────┴─────┴───────┴──────┴──────┘
```

Here, `"median"` is a convenience string that is equivalent to the more
verbose `pl$element()$median()`. Other convenience strings include
“first”, “last”, “min”, “max”, “mean”, “sum”, and “count”.

## Join

As a final example of how **polars** can be used for standard data
wrangling tasks, let’s implement a (left) join. For this example, we’ll
borrow some datasets from the **nycflights13** package.

``` r
data("flights", "planes", package = "nycflights13")
flights = as_polars_df(flights)
planes = as_polars_df(planes)

flights$join(
  planes,
  on = "tailnum",
  how = "left"
)
#> shape: (336_776, 27)
#> ┌──────┬───────┬─────┬──────────┬───┬─────────┬───────┬───────┬───────────┐
#> │ year ┆ month ┆ day ┆ dep_time ┆ … ┆ engines ┆ seats ┆ speed ┆ engine    │
#> │ ---  ┆ ---   ┆ --- ┆ ---      ┆   ┆ ---     ┆ ---   ┆ ---   ┆ ---       │
#> │ i32  ┆ i32   ┆ i32 ┆ i32      ┆   ┆ i32     ┆ i32   ┆ i32   ┆ str       │
#> ╞══════╪═══════╪═════╪══════════╪═══╪═════════╪═══════╪═══════╪═══════════╡
#> │ 2013 ┆ 1     ┆ 1   ┆ 517      ┆ … ┆ 2       ┆ 149   ┆ null  ┆ Turbo-fan │
#> │ 2013 ┆ 1     ┆ 1   ┆ 533      ┆ … ┆ 2       ┆ 149   ┆ null  ┆ Turbo-fan │
#> │ 2013 ┆ 1     ┆ 1   ┆ 542      ┆ … ┆ 2       ┆ 178   ┆ null  ┆ Turbo-fan │
#> │ 2013 ┆ 1     ┆ 1   ┆ 544      ┆ … ┆ 2       ┆ 200   ┆ null  ┆ Turbo-fan │
#> │ 2013 ┆ 1     ┆ 1   ┆ 554      ┆ … ┆ 2       ┆ 178   ┆ null  ┆ Turbo-fan │
#> │ …    ┆ …     ┆ …   ┆ …        ┆ … ┆ …       ┆ …     ┆ …     ┆ …         │
#> │ 2013 ┆ 9     ┆ 30  ┆ null     ┆ … ┆ null    ┆ null  ┆ null  ┆ null      │
#> │ 2013 ┆ 9     ┆ 30  ┆ null     ┆ … ┆ null    ┆ null  ┆ null  ┆ null      │
#> │ 2013 ┆ 9     ┆ 30  ┆ null     ┆ … ┆ null    ┆ null  ┆ null  ┆ null      │
#> │ 2013 ┆ 9     ┆ 30  ┆ null     ┆ … ┆ null    ┆ null  ┆ null  ┆ null      │
#> │ 2013 ┆ 9     ┆ 30  ┆ null     ┆ … ┆ null    ┆ null  ┆ null  ┆ null      │
#> └──────┴───────┴─────┴──────────┴───┴─────────┴───────┴───────┴───────────┘
```

More information on the **polars** joining method can be found in the
[reference manual](https://rpolars.github.io/man/DataFrame_join.html).

The package supports many other data manipulation operations, which we
won’t cover here. Hopefully, you will already have a sense of the key
syntax features. We now turn to another core idea of the Polars
ecosystem: *lazy execution*.

## Lazy execution

While the “eager” execution engine of **polars** works perfectly well—as
evidenced by all of the previous examples—to get the most out of the
package you need to go *lazy*. Lazy execution enables several benefits,
but the most important is that it improves performance. Delaying
execution until the last possible moment allows Polars to apply
automatic optimization to every query. Let’s take a quick look.

To create a so-called
“[LazyFrame](https://rpolars.github.io/man/LazyFrame_class.html)” from
an existing object in memory, we can invoke the `lazy()` constructor.

``` r
ldat = dat$lazy()
ldat
#> [1] "polars LazyFrame naive plan: (run ldf$describe_optimized_plan() to see the optimized plan)"
#> DF ["mpg", "cyl", "disp", "hp"]; PROJECT */11 COLUMNS; SELECTION: "None"
```

Or, use the `as_polars_lf()` generic function.

``` r
as_polars_lf(dat)
#> [1] "polars LazyFrame naive plan: (run ldf$describe_optimized_plan() to see the optimized plan)"
#> DF ["mpg", "cyl", "disp", "hp"]; PROJECT */11 COLUMNS; SELECTION: "None"
```

Now consider what happens when we run our subsetting query from earlier
on this LazyFrame.

``` r
subset_query = ldat$filter(
  pl$col("cyl") == 6
)$select(
  pl$col(c("mpg", "hp", "cyl"))
)

subset_query
#> [1] "polars LazyFrame naive plan: (run ldf$describe_optimized_plan() to see the optimized plan)"
#>  SELECT [col("mpg"), col("hp"), col("cyl")] FROM
#>   FILTER [(col("cyl")) == (6.0)] FROM
#> 
#>   DF ["mpg", "cyl", "disp", "hp"]; PROJECT */11 COLUMNS; SELECTION: "None"
```

Right now we only have a tree of instructions. But underneath the hood,
Polars has already worked out a more optimized version of the query. We
can view this optimized plan this by requesting it.

``` r
subset_query$describe_optimized_plan()
#> FAST_PROJECT: [mpg, hp, cyl]
#>   DF ["mpg", "cyl", "disp", "hp"]; PROJECT 3/11 COLUMNS; SELECTION: "[(col(\"cyl\")) == (6.0)]"
```

Here we see a simple, but surprisingly effective component in query
optimization: *projection*. Changing the order in which our subsetting
operations occurs—in this case, subsetting on columns first—reduces the
memory overhead of the overall query and leads to a downstream speedup.
Of course, you would hardly notice a difference for this small dataset.
But the same principles carry over to much bigger datasets and more
complex queries.

To actually execute the plan, we just need to invoke the `collect()`
method. This should feel very familiar if you have previously used other
lazy execution engines like those provided by **arrow** or **dbplyr**.

``` r
subset_query$collect()
#> shape: (7, 3)
#> ┌──────┬───────┬─────┐
#> │ mpg  ┆ hp    ┆ cyl │
#> │ ---  ┆ ---   ┆ --- │
#> │ f64  ┆ f64   ┆ f64 │
#> ╞══════╪═══════╪═════╡
#> │ 21.0 ┆ 110.0 ┆ 6.0 │
#> │ 21.0 ┆ 110.0 ┆ 6.0 │
#> │ 21.4 ┆ 110.0 ┆ 6.0 │
#> │ 18.1 ┆ 105.0 ┆ 6.0 │
#> │ 19.2 ┆ 123.0 ┆ 6.0 │
#> │ 17.8 ┆ 123.0 ┆ 6.0 │
#> │ 19.7 ┆ 175.0 ┆ 6.0 │
#> └──────┴───────┴─────┘
```

## Data import

**polars** supports data import of both CSV and Parquet files formats.
Here we demonstrate using the `airquality` dataset that also comes
bundled with base R.

``` r
write.csv(airquality, "airquality.csv", row.names = FALSE)

pl$read_csv("airquality.csv")
#> shape: (153, 6)
#> ┌───────┬─────────┬──────┬──────┬───────┬─────┐
#> │ Ozone ┆ Solar.R ┆ Wind ┆ Temp ┆ Month ┆ Day │
#> │ ---   ┆ ---     ┆ ---  ┆ ---  ┆ ---   ┆ --- │
#> │ str   ┆ str     ┆ f64  ┆ i64  ┆ i64   ┆ i64 │
#> ╞═══════╪═════════╪══════╪══════╪═══════╪═════╡
#> │ 41    ┆ 190     ┆ 7.4  ┆ 67   ┆ 5     ┆ 1   │
#> │ 36    ┆ 118     ┆ 8.0  ┆ 72   ┆ 5     ┆ 2   │
#> │ 12    ┆ 149     ┆ 12.6 ┆ 74   ┆ 5     ┆ 3   │
#> │ 18    ┆ 313     ┆ 11.5 ┆ 62   ┆ 5     ┆ 4   │
#> │ NA    ┆ NA      ┆ 14.3 ┆ 56   ┆ 5     ┆ 5   │
#> │ …     ┆ …       ┆ …    ┆ …    ┆ …     ┆ …   │
#> │ 30    ┆ 193     ┆ 6.9  ┆ 70   ┆ 9     ┆ 26  │
#> │ NA    ┆ 145     ┆ 13.2 ┆ 77   ┆ 9     ┆ 27  │
#> │ 14    ┆ 191     ┆ 14.3 ┆ 75   ┆ 9     ┆ 28  │
#> │ 18    ┆ 131     ┆ 8.0  ┆ 76   ┆ 9     ┆ 29  │
#> │ 20    ┆ 223     ┆ 11.5 ┆ 68   ┆ 9     ┆ 30  │
#> └───────┴─────────┴──────┴──────┴───────┴─────┘
```

Again, however, the package works best if we take the lazy approach.

``` r
pl$scan_csv("airquality.csv")
#> [1] "polars LazyFrame naive plan: (run ldf$describe_optimized_plan() to see the optimized plan)"
#> 
#>   Csv SCAN airquality.csv
#>   PROJECT */6 COLUMNS
```

We could obviously append a set of query operators to the above
LazyFrame and then collect the results. However, this workflow is even
better suited to Parquet files, since we can leverage their efficient
storage format on disk. Let’s see an example.

``` r
as_polars_df(airquality)$write_parquet("airquality.parquet")

# eager version (okay)
aq_collected = pl$read_parquet("airquality.parquet")

# lazy version (better)
aq = pl$scan_parquet("airquality.parquet")

aq$filter(
  pl$col("Month") <= 6
)$group_by(
  "Month"
)$agg(
  pl$col(c("Ozone", "Temp"))$mean()
)$collect()
#> shape: (2, 3)
#> ┌───────┬───────────┬───────────┐
#> │ Month ┆ Ozone     ┆ Temp      │
#> │ ---   ┆ ---       ┆ ---       │
#> │ i32   ┆ f64       ┆ f64       │
#> ╞═══════╪═══════════╪═══════════╡
#> │ 6     ┆ 29.444444 ┆ 79.1      │
#> │ 5     ┆ 23.615385 ┆ 65.548387 │
#> └───────┴───────────┴───────────┘
```

Finally, we can read/scan multiple files in the same directory through
pattern globbing.

``` r
dir.create("airquality-ds")

# Create a hive-partitioned dataset with the function from the arrow package
arrow::write_dataset(airquality, "airquality-ds", partitioning = "Month")

# Use pattern globbing to scan all parquet files in the folder
aq2 = pl$scan_parquet("airquality-ds/**/*.parquet")

# Just print the first two rows.
aq2$limit(2)$collect()
#> shape: (2, 6)
#> ┌───────┬─────────┬──────┬──────┬─────┬───────┐
#> │ Ozone ┆ Solar.R ┆ Wind ┆ Temp ┆ Day ┆ Month │
#> │ ---   ┆ ---     ┆ ---  ┆ ---  ┆ --- ┆ ---   │
#> │ i32   ┆ i32     ┆ f64  ┆ i32  ┆ i32 ┆ i64   │
#> ╞═══════╪═════════╪══════╪══════╪═════╪═══════╡
#> │ 41    ┆ 190     ┆ 7.4  ┆ 67   ┆ 1   ┆ 5     │
#> │ 36    ┆ 118     ┆ 8.0  ┆ 72   ┆ 2   ┆ 5     │
#> └───────┴─────────┴──────┴──────┴─────┴───────┘
```

Before continuing, don’t forget to clean up by removing the newly
created temp files and directory on disk.

``` r
file.remove(c("airquality.csv", "airquality.parquet"))
#> [1] TRUE TRUE
unlink("airquality-ds", recursive = TRUE)
```

## Execute R functions within a Polars query

It is possible to mix R code with Polars by passing R functions to
**polars**. This can unlock a lot of flexibility, but note that it can
inhibit performance. R functions are typically slower, so we recommend
using native Polars functions and expressions wherever possible.

``` r
as_polars_df(iris)$select(
  pl$col("Sepal.Length")$map_batches(\(s) { # map with a R function
    x = s$to_vector() # convert from Polars Series to a native R vector
    x[x >= 5] = 10
    x[1:10] # if return is R vector, it will automatically be converted to Polars Series again
  })
) |>
  as.data.frame()
#>    Sepal.Length
#> 1          10.0
#> 2           4.9
#> 3           4.7
#> 4           4.6
#> 5          10.0
#> 6          10.0
#> 7           4.6
#> 8          10.0
#> 9           4.4
#> 10          4.9
```

## Data types

Polars is [strongly
typed](https://en.wikipedia.org/wiki/Strong_and_weak_typing) and new
types can be created with the `dtypes` constructor. For example:

``` r
pl$dtypes$Float64
#> DataType: Float64
```

The full list of valid Polars types can be found by typing `pl$dtypes`
into your R console. These include *Boolean*, *Float32(64)*,
*Int32(64)*, *Utf8*, *Categorical*, *Date*, etc. Note that some type
names differ from what they are called in R (e.g., *Boolean* in Polars
is equivalent to `logical()` in R). This might occasionally require you
to look up a specific type. But the good news is that **polars**
generally does a good job of inferring types automatically.

[1] Similar to how (most) **data.table** operations are limited to
objects of class `data.table`, we can only perform polars operations on
objects that have been converted to an appropriate **polars** class.
Later on, we’ll see how to read data from disk directly in Polars
format.
