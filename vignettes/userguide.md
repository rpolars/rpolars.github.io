# Polars - User Guide for R


[The Polars User
Guide](https://pola-rs.github.io/polars-book/user-guide/) is a detailed
tutorial about the Polars DataFrame library. Its goal is to introduce
you to Polars by going through examples and comparing it to other
solutions. Some design choices are introduced there. The guide also
introduces you to optimal usage of Polars. The Polars User Guide is
available at this link:

https://pola-rs.github.io/polars-book/user-guide/

Currently, the User Guide includes code examples in Python and Rust.
This page complements the guide with examples in R. The R examples are
not complete yet; when they are complete, our goal is to merge them into
the main User Guide. If you want to help, please submit a pull request
to the [R polars Github
repository.](https://github.com/pola-rs/r-polars)

The current page works as a reference document, for side-by-side
comparisons with the Python and Rust examples in the main User Guide.

# Introduction

``` r
library(polars)
```

# Getting started

``` r
df = pl$read_csv("https://j.mp/iriscsv")
```

``` r
df$filter(pl$col("sepal_length") > 5)$
  group_by("species", maintain_order = TRUE)$
  agg(pl$all()$sum())
#> shape: (3, 5)
#> ┌────────────┬──────────────┬─────────────┬──────────────┬─────────────┐
#> │ species    ┆ sepal_length ┆ sepal_width ┆ petal_length ┆ petal_width │
#> │ ---        ┆ ---          ┆ ---         ┆ ---          ┆ ---         │
#> │ str        ┆ f64          ┆ f64         ┆ f64          ┆ f64         │
#> ╞════════════╪══════════════╪═════════════╪══════════════╪═════════════╡
#> │ setosa     ┆ 116.9        ┆ 81.7        ┆ 33.2         ┆ 6.1         │
#> │ versicolor ┆ 281.9        ┆ 131.8       ┆ 202.9        ┆ 63.3        │
#> │ virginica  ┆ 324.5        ┆ 146.2       ┆ 273.1        ┆ 99.6        │
#> └────────────┴──────────────┴─────────────┴──────────────┴─────────────┘

df$
  lazy()$
  filter(pl$col("sepal_length") > 5)$
  group_by("species", maintain_order = TRUE)$
  agg(pl$all()$sum())$
  collect()
#> shape: (3, 5)
#> ┌────────────┬──────────────┬─────────────┬──────────────┬─────────────┐
#> │ species    ┆ sepal_length ┆ sepal_width ┆ petal_length ┆ petal_width │
#> │ ---        ┆ ---          ┆ ---         ┆ ---          ┆ ---         │
#> │ str        ┆ f64          ┆ f64         ┆ f64          ┆ f64         │
#> ╞════════════╪══════════════╪═════════════╪══════════════╪═════════════╡
#> │ setosa     ┆ 116.9        ┆ 81.7        ┆ 33.2         ┆ 6.1         │
#> │ versicolor ┆ 281.9        ┆ 131.8       ┆ 202.9        ┆ 63.3        │
#> │ virginica  ┆ 324.5        ┆ 146.2       ┆ 273.1        ┆ 99.6        │
#> └────────────┴──────────────┴─────────────┴──────────────┴─────────────┘
```

# Polars quick exploration guide

``` r
series = pl$Series(c(1, 2, 3, 4, 5))
series
#> polars Series: shape: (5,)
#> Series: '' [f64]
#> [
#>  1.0
#>  2.0
#>  3.0
#>  4.0
#>  5.0
#> ]

df = pl$DataFrame(
  "integer" = c(1, 2, 3),
  "date" = as.Date(c("2022-1-1", "2022-1-2", "2022-1-3")),
  "float" = c(4.0, 5.0, 6.0))
df
#> shape: (3, 3)
#> ┌─────────┬────────────┬───────┐
#> │ integer ┆ date       ┆ float │
#> │ ---     ┆ ---        ┆ ---   │
#> │ f64     ┆ date       ┆ f64   │
#> ╞═════════╪════════════╪═══════╡
#> │ 1.0     ┆ 2022-01-01 ┆ 4.0   │
#> │ 2.0     ┆ 2022-01-02 ┆ 5.0   │
#> │ 3.0     ┆ 2022-01-03 ┆ 6.0   │
#> └─────────┴────────────┴───────┘

# df$write_csv('output.csv')
# df_csv_with_dates = pl$read_csv("output.csv", parse_dates=True)
# print(df_csv_with_dates)

# dataframe$write_json('output.json')
# df_json = pl$read_json("output.json")
# print(df_json)

# dataframe$write_parquet('output.parquet')
# df_parquet = pl$read_parquet("output.parquet")
# print(df_parquet)

df = pl$DataFrame(
  "a" = as.numeric(0:7),
  "b" = runif(8),
  "c" = as.Date(sprintf("2022-12-%s", 1:8)),
  "d" = c(1, 2.0, NaN, NaN, 0, -5, -42, NA)
)
df$head(5)
#> shape: (5, 4)
#> ┌─────┬──────────┬────────────┬─────┐
#> │ a   ┆ b        ┆ c          ┆ d   │
#> │ --- ┆ ---      ┆ ---        ┆ --- │
#> │ f64 ┆ f64      ┆ date       ┆ f64 │
#> ╞═════╪══════════╪════════════╪═════╡
#> │ 0.0 ┆ 0.594998 ┆ 2022-12-01 ┆ 1.0 │
#> │ 1.0 ┆ 0.921552 ┆ 2022-12-02 ┆ 2.0 │
#> │ 2.0 ┆ 0.348083 ┆ 2022-12-03 ┆ NaN │
#> │ 3.0 ┆ 0.59448  ┆ 2022-12-04 ┆ NaN │
#> │ 4.0 ┆ 0.080723 ┆ 2022-12-05 ┆ 0.0 │
#> └─────┴──────────┴────────────┴─────┘

df$tail(5)
#> shape: (5, 4)
#> ┌─────┬──────────┬────────────┬───────┐
#> │ a   ┆ b        ┆ c          ┆ d     │
#> │ --- ┆ ---      ┆ ---        ┆ ---   │
#> │ f64 ┆ f64      ┆ date       ┆ f64   │
#> ╞═════╪══════════╪════════════╪═══════╡
#> │ 3.0 ┆ 0.59448  ┆ 2022-12-04 ┆ NaN   │
#> │ 4.0 ┆ 0.080723 ┆ 2022-12-05 ┆ 0.0   │
#> │ 5.0 ┆ 0.123556 ┆ 2022-12-06 ┆ -5.0  │
#> │ 6.0 ┆ 0.56115  ┆ 2022-12-07 ┆ -42.0 │
#> │ 7.0 ┆ 0.183902 ┆ 2022-12-08 ┆ null  │
#> └─────┴──────────┴────────────┴───────┘

## not implemented yet
# df$sample(3)

## not implemented yet
# df$describe()

df$select(pl$col("*"))
#> shape: (8, 4)
#> ┌─────┬──────────┬────────────┬───────┐
#> │ a   ┆ b        ┆ c          ┆ d     │
#> │ --- ┆ ---      ┆ ---        ┆ ---   │
#> │ f64 ┆ f64      ┆ date       ┆ f64   │
#> ╞═════╪══════════╪════════════╪═══════╡
#> │ 0.0 ┆ 0.594998 ┆ 2022-12-01 ┆ 1.0   │
#> │ 1.0 ┆ 0.921552 ┆ 2022-12-02 ┆ 2.0   │
#> │ 2.0 ┆ 0.348083 ┆ 2022-12-03 ┆ NaN   │
#> │ 3.0 ┆ 0.59448  ┆ 2022-12-04 ┆ NaN   │
#> │ 4.0 ┆ 0.080723 ┆ 2022-12-05 ┆ 0.0   │
#> │ 5.0 ┆ 0.123556 ┆ 2022-12-06 ┆ -5.0  │
#> │ 6.0 ┆ 0.56115  ┆ 2022-12-07 ┆ -42.0 │
#> │ 7.0 ┆ 0.183902 ┆ 2022-12-08 ┆ null  │
#> └─────┴──────────┴────────────┴───────┘

df$select(pl$col(c("a", "b")))
#> shape: (8, 2)
#> ┌─────┬──────────┐
#> │ a   ┆ b        │
#> │ --- ┆ ---      │
#> │ f64 ┆ f64      │
#> ╞═════╪══════════╡
#> │ 0.0 ┆ 0.594998 │
#> │ 1.0 ┆ 0.921552 │
#> │ 2.0 ┆ 0.348083 │
#> │ 3.0 ┆ 0.59448  │
#> │ 4.0 ┆ 0.080723 │
#> │ 5.0 ┆ 0.123556 │
#> │ 6.0 ┆ 0.56115  │
#> │ 7.0 ┆ 0.183902 │
#> └─────┴──────────┘

df$select(pl$col(c("a", "b")))
#> shape: (8, 2)
#> ┌─────┬──────────┐
#> │ a   ┆ b        │
#> │ --- ┆ ---      │
#> │ f64 ┆ f64      │
#> ╞═════╪══════════╡
#> │ 0.0 ┆ 0.594998 │
#> │ 1.0 ┆ 0.921552 │
#> │ 2.0 ┆ 0.348083 │
#> │ 3.0 ┆ 0.59448  │
#> │ 4.0 ┆ 0.080723 │
#> │ 5.0 ┆ 0.123556 │
#> │ 6.0 ┆ 0.56115  │
#> │ 7.0 ┆ 0.183902 │
#> └─────┴──────────┘

df$select(pl$col("a"), pl$col("b"))$limit(3)
#> shape: (3, 2)
#> ┌─────┬──────────┐
#> │ a   ┆ b        │
#> │ --- ┆ ---      │
#> │ f64 ┆ f64      │
#> ╞═════╪══════════╡
#> │ 0.0 ┆ 0.594998 │
#> │ 1.0 ┆ 0.921552 │
#> │ 2.0 ┆ 0.348083 │
#> └─────┴──────────┘

df$select(pl$all()$exclude("a"))
#> shape: (8, 3)
#> ┌──────────┬────────────┬───────┐
#> │ b        ┆ c          ┆ d     │
#> │ ---      ┆ ---        ┆ ---   │
#> │ f64      ┆ date       ┆ f64   │
#> ╞══════════╪════════════╪═══════╡
#> │ 0.594998 ┆ 2022-12-01 ┆ 1.0   │
#> │ 0.921552 ┆ 2022-12-02 ┆ 2.0   │
#> │ 0.348083 ┆ 2022-12-03 ┆ NaN   │
#> │ 0.59448  ┆ 2022-12-04 ┆ NaN   │
#> │ 0.080723 ┆ 2022-12-05 ┆ 0.0   │
#> │ 0.123556 ┆ 2022-12-06 ┆ -5.0  │
#> │ 0.56115  ┆ 2022-12-07 ┆ -42.0 │
#> │ 0.183902 ┆ 2022-12-08 ┆ null  │
#> └──────────┴────────────┴───────┘

df$filter(
    pl$col("c")$is_between(as.Date("2022-12-2"), as.Date("2022-12-8"))
)
#> shape: (5, 4)
#> ┌─────┬──────────┬────────────┬───────┐
#> │ a   ┆ b        ┆ c          ┆ d     │
#> │ --- ┆ ---      ┆ ---        ┆ ---   │
#> │ f64 ┆ f64      ┆ date       ┆ f64   │
#> ╞═════╪══════════╪════════════╪═══════╡
#> │ 2.0 ┆ 0.348083 ┆ 2022-12-03 ┆ NaN   │
#> │ 3.0 ┆ 0.59448  ┆ 2022-12-04 ┆ NaN   │
#> │ 4.0 ┆ 0.080723 ┆ 2022-12-05 ┆ 0.0   │
#> │ 5.0 ┆ 0.123556 ┆ 2022-12-06 ┆ -5.0  │
#> │ 6.0 ┆ 0.56115  ┆ 2022-12-07 ┆ -42.0 │
#> └─────┴──────────┴────────────┴───────┘

df$filter((pl$col("a") <= 3) & (pl$col("d")$is_not_nan()))
#> shape: (2, 4)
#> ┌─────┬──────────┬────────────┬─────┐
#> │ a   ┆ b        ┆ c          ┆ d   │
#> │ --- ┆ ---      ┆ ---        ┆ --- │
#> │ f64 ┆ f64      ┆ date       ┆ f64 │
#> ╞═════╪══════════╪════════════╪═════╡
#> │ 0.0 ┆ 0.594998 ┆ 2022-12-01 ┆ 1.0 │
#> │ 1.0 ┆ 0.921552 ┆ 2022-12-02 ┆ 2.0 │
#> └─────┴──────────┴────────────┴─────┘

df$with_columns(pl$col("b")$sum()$alias("e"), (pl$col("b") + 42)$alias("b+42"))
#> shape: (8, 6)
#> ┌─────┬──────────┬────────────┬───────┬──────────┬───────────┐
#> │ a   ┆ b        ┆ c          ┆ d     ┆ e        ┆ b+42      │
#> │ --- ┆ ---      ┆ ---        ┆ ---   ┆ ---      ┆ ---       │
#> │ f64 ┆ f64      ┆ date       ┆ f64   ┆ f64      ┆ f64       │
#> ╞═════╪══════════╪════════════╪═══════╪══════════╪═══════════╡
#> │ 0.0 ┆ 0.594998 ┆ 2022-12-01 ┆ 1.0   ┆ 3.408444 ┆ 42.594998 │
#> │ 1.0 ┆ 0.921552 ┆ 2022-12-02 ┆ 2.0   ┆ 3.408444 ┆ 42.921552 │
#> │ 2.0 ┆ 0.348083 ┆ 2022-12-03 ┆ NaN   ┆ 3.408444 ┆ 42.348083 │
#> │ 3.0 ┆ 0.59448  ┆ 2022-12-04 ┆ NaN   ┆ 3.408444 ┆ 42.59448  │
#> │ 4.0 ┆ 0.080723 ┆ 2022-12-05 ┆ 0.0   ┆ 3.408444 ┆ 42.080723 │
#> │ 5.0 ┆ 0.123556 ┆ 2022-12-06 ┆ -5.0  ┆ 3.408444 ┆ 42.123556 │
#> │ 6.0 ┆ 0.56115  ┆ 2022-12-07 ┆ -42.0 ┆ 3.408444 ┆ 42.56115  │
#> │ 7.0 ┆ 0.183902 ┆ 2022-12-08 ┆ null  ┆ 3.408444 ┆ 42.183902 │
#> └─────┴──────────┴────────────┴───────┴──────────┴───────────┘

df$with_columns((pl$col("a") * pl$col("b"))$alias("a * b"))$select(pl$all()$exclude(c("c", "d")))
#> shape: (8, 3)
#> ┌─────┬──────────┬──────────┐
#> │ a   ┆ b        ┆ a * b    │
#> │ --- ┆ ---      ┆ ---      │
#> │ f64 ┆ f64      ┆ f64      │
#> ╞═════╪══════════╪══════════╡
#> │ 0.0 ┆ 0.594998 ┆ 0.0      │
#> │ 1.0 ┆ 0.921552 ┆ 0.921552 │
#> │ 2.0 ┆ 0.348083 ┆ 0.696167 │
#> │ 3.0 ┆ 0.59448  ┆ 1.783441 │
#> │ 4.0 ┆ 0.080723 ┆ 0.322891 │
#> │ 5.0 ┆ 0.123556 ┆ 0.617782 │
#> │ 6.0 ┆ 0.56115  ┆ 3.3669   │
#> │ 7.0 ┆ 0.183902 ┆ 1.287314 │
#> └─────┴──────────┴──────────┘

df = pl$DataFrame("x" = 0:7, "y" = c("A", "A", "A", "B", "B", "C", "X", "X"))

df$
  group_by("y", maintain_order = FALSE)$
  agg(
    pl$col("*")$count()$alias("count"),
    pl$col("*")$sum()$alias("sum")
  )
#> shape: (4, 3)
#> ┌─────┬───────┬─────┐
#> │ y   ┆ count ┆ sum │
#> │ --- ┆ ---   ┆ --- │
#> │ str ┆ u32   ┆ i32 │
#> ╞═════╪═══════╪═════╡
#> │ A   ┆ 3     ┆ 3   │
#> │ C   ┆ 1     ┆ 5   │
#> │ X   ┆ 2     ┆ 13  │
#> │ B   ┆ 2     ┆ 7   │
#> └─────┴───────┴─────┘

df1 = pl$DataFrame(
  "a" = 0:7,
  "b" = runif(8),
  "c" = as.Date(sprintf("2022-12-%s", 1:8)),
  "d" = c(1, 2.0, NaN, NaN, 0, -5, -42, NA)
)
df2 = pl$DataFrame("x" = 0:7, "y" = c("A", "A", "A", "B", "B", "C", "X", "X"))

pl$concat(c(df1, df2), how = "horizontal")
#> shape: (8, 6)
#> ┌─────┬──────────┬────────────┬───────┬─────┬─────┐
#> │ a   ┆ b        ┆ c          ┆ d     ┆ x   ┆ y   │
#> │ --- ┆ ---      ┆ ---        ┆ ---   ┆ --- ┆ --- │
#> │ i32 ┆ f64      ┆ date       ┆ f64   ┆ i32 ┆ str │
#> ╞═════╪══════════╪════════════╪═══════╪═════╪═════╡
#> │ 0   ┆ 0.474311 ┆ 2022-12-01 ┆ 1.0   ┆ 0   ┆ A   │
#> │ 1   ┆ 0.588773 ┆ 2022-12-02 ┆ 2.0   ┆ 1   ┆ A   │
#> │ 2   ┆ 0.082627 ┆ 2022-12-03 ┆ NaN   ┆ 2   ┆ A   │
#> │ 3   ┆ 0.173685 ┆ 2022-12-04 ┆ NaN   ┆ 3   ┆ B   │
#> │ 4   ┆ 0.362373 ┆ 2022-12-05 ┆ 0.0   ┆ 4   ┆ B   │
#> │ 5   ┆ 0.728771 ┆ 2022-12-06 ┆ -5.0  ┆ 5   ┆ C   │
#> │ 6   ┆ 0.244295 ┆ 2022-12-07 ┆ -42.0 ┆ 6   ┆ X   │
#> │ 7   ┆ 0.239526 ┆ 2022-12-08 ┆ null  ┆ 7   ┆ X   │
#> └─────┴──────────┴────────────┴───────┴─────┴─────┘
```

# Polars expressions

## Expressions

``` r
df = pl$DataFrame(
  "nrs" = c(1, 2, 3, NA, 5),
  "names" = c("foo", "ham", "spam", "egg", NA),
  "random" = runif(5),
  "groups" = c("A", "A", "B", "C", "B")
)
df
#> shape: (5, 4)
#> ┌──────┬───────┬──────────┬────────┐
#> │ nrs  ┆ names ┆ random   ┆ groups │
#> │ ---  ┆ ---   ┆ ---      ┆ ---    │
#> │ f64  ┆ str   ┆ f64      ┆ str    │
#> ╞══════╪═══════╪══════════╪════════╡
#> │ 1.0  ┆ foo   ┆ 0.668956 ┆ A      │
#> │ 2.0  ┆ ham   ┆ 0.977133 ┆ A      │
#> │ 3.0  ┆ spam  ┆ 0.574689 ┆ B      │
#> │ null ┆ egg   ┆ 0.734675 ┆ C      │
#> │ 5.0  ┆ null  ┆ 0.102994 ┆ B      │
#> └──────┴───────┴──────────┴────────┘

df$select(
  pl$col("names")$n_unique()$alias("unique_names_1"),
  pl$col("names")$unique()$count()$alias("unique_names_2")
)
#> shape: (1, 2)
#> ┌────────────────┬────────────────┐
#> │ unique_names_1 ┆ unique_names_2 │
#> │ ---            ┆ ---            │
#> │ u32            ┆ u32            │
#> ╞════════════════╪════════════════╡
#> │ 5              ┆ 4              │
#> └────────────────┴────────────────┘

df$select(
  pl$sum("random")$alias("sum"),
  pl$min("random")$alias("min"),
  pl$max("random")$alias("max"),
  pl$col("random")$max()$alias("other_max"),
  pl$std("random")$alias("std dev"),
  pl$var("random")$alias("variance")
)
#> shape: (1, 6)
#> ┌──────────┬──────────┬──────────┬───────────┬──────────┬──────────┐
#> │ sum      ┆ min      ┆ max      ┆ other_max ┆ std dev  ┆ variance │
#> │ ---      ┆ ---      ┆ ---      ┆ ---       ┆ ---      ┆ ---      │
#> │ f64      ┆ f64      ┆ f64      ┆ f64       ┆ f64      ┆ f64      │
#> ╞══════════╪══════════╪══════════╪═══════════╪══════════╪══════════╡
#> │ 3.058448 ┆ 0.102994 ┆ 0.977133 ┆ 0.977133  ┆ 0.320973 ┆ 0.103023 │
#> └──────────┴──────────┴──────────┴───────────┴──────────┴──────────┘

df$select(
  pl$col("names")$filter(pl$col("names")$str$contains("am$"))$count()
)
#> shape: (1, 1)
#> ┌───────┐
#> │ names │
#> │ ---   │
#> │ u32   │
#> ╞═══════╡
#> │ 2     │
#> └───────┘

df$select(
  pl$when(pl$col("random") > 0.5)$then(0)$otherwise(pl$col("random")) * pl$sum("nrs")
)
#> shape: (5, 1)
#> ┌──────────┐
#> │ literal  │
#> │ ---      │
#> │ f64      │
#> ╞══════════╡
#> │ 0.0      │
#> │ 0.0      │
#> │ 0.0      │
#> │ 0.0      │
#> │ 1.132936 │
#> └──────────┘

df$select(
  pl$when(pl$col("groups") == "A")$then(1)$when(pl$col("random") > 0.5)$then(0)$otherwise(pl$col("random"))
)
#> shape: (5, 1)
#> ┌──────────┐
#> │ literal  │
#> │ ---      │
#> │ f64      │
#> ╞══════════╡
#> │ 1.0      │
#> │ 1.0      │
#> │ 0.0      │
#> │ 0.0      │
#> │ 0.102994 │
#> └──────────┘

df$select(
  pl$col("*"),  # select all
  pl$col("random")$sum()$over("groups")$alias("sumc(random)/groups"),
  pl$col("random")$implode()$over("names")$alias("random/name")
)
#> shape: (5, 6)
#> ┌──────┬───────┬──────────┬────────┬─────────────────────┬─────────────┐
#> │ nrs  ┆ names ┆ random   ┆ groups ┆ sumc(random)/groups ┆ random/name │
#> │ ---  ┆ ---   ┆ ---      ┆ ---    ┆ ---                 ┆ ---         │
#> │ f64  ┆ str   ┆ f64      ┆ str    ┆ f64                 ┆ list[f64]   │
#> ╞══════╪═══════╪══════════╪════════╪═════════════════════╪═════════════╡
#> │ 1.0  ┆ foo   ┆ 0.668956 ┆ A      ┆ 1.64609             ┆ [0.668956]  │
#> │ 2.0  ┆ ham   ┆ 0.977133 ┆ A      ┆ 1.64609             ┆ [0.977133]  │
#> │ 3.0  ┆ spam  ┆ 0.574689 ┆ B      ┆ 0.677683            ┆ [0.574689]  │
#> │ null ┆ egg   ┆ 0.734675 ┆ C      ┆ 0.734675            ┆ [0.734675]  │
#> │ 5.0  ┆ null  ┆ 0.102994 ┆ B      ┆ 0.677683            ┆ [0.102994]  │
#> └──────┴───────┴──────────┴────────┴─────────────────────┴─────────────┘
```

## Contexts

``` r
df$select(
  pl$sum("nrs"),
  pl$col("names")$sort(),
  pl$col("names")$first()$alias("first name"),
  (pl$mean("nrs") * 10)$alias("10xnrs")
)
#> shape: (5, 4)
#> ┌──────┬───────┬────────────┬────────┐
#> │ nrs  ┆ names ┆ first name ┆ 10xnrs │
#> │ ---  ┆ ---   ┆ ---        ┆ ---    │
#> │ f64  ┆ str   ┆ str        ┆ f64    │
#> ╞══════╪═══════╪════════════╪════════╡
#> │ 11.0 ┆ null  ┆ foo        ┆ 27.5   │
#> │ 11.0 ┆ egg   ┆ foo        ┆ 27.5   │
#> │ 11.0 ┆ foo   ┆ foo        ┆ 27.5   │
#> │ 11.0 ┆ ham   ┆ foo        ┆ 27.5   │
#> │ 11.0 ┆ spam  ┆ foo        ┆ 27.5   │
#> └──────┴───────┴────────────┴────────┘

df$with_columns(
  pl$sum("nrs")$alias("nrs_sum"),
  pl$col("random")$count()$alias("count")
)
#> shape: (5, 6)
#> ┌──────┬───────┬──────────┬────────┬─────────┬───────┐
#> │ nrs  ┆ names ┆ random   ┆ groups ┆ nrs_sum ┆ count │
#> │ ---  ┆ ---   ┆ ---      ┆ ---    ┆ ---     ┆ ---   │
#> │ f64  ┆ str   ┆ f64      ┆ str    ┆ f64     ┆ u32   │
#> ╞══════╪═══════╪══════════╪════════╪═════════╪═══════╡
#> │ 1.0  ┆ foo   ┆ 0.668956 ┆ A      ┆ 11.0    ┆ 5     │
#> │ 2.0  ┆ ham   ┆ 0.977133 ┆ A      ┆ 11.0    ┆ 5     │
#> │ 3.0  ┆ spam  ┆ 0.574689 ┆ B      ┆ 11.0    ┆ 5     │
#> │ null ┆ egg   ┆ 0.734675 ┆ C      ┆ 11.0    ┆ 5     │
#> │ 5.0  ┆ null  ┆ 0.102994 ┆ B      ┆ 11.0    ┆ 5     │
#> └──────┴───────┴──────────┴────────┴─────────┴───────┘

df$group_by("groups")$agg(
  pl$sum("nrs"),  # sum nrs by groups
  pl$col("random")$count()$alias("count"),  # count group members
  # sum random where name != null
  pl$col("random")$filter(pl$col("names")$is_not_null())$sum()$name$suffix("_sum"),
  pl$col("names")$reverse()$alias(("reversed names"))
)
#> shape: (3, 5)
#> ┌────────┬─────┬───────┬────────────┬────────────────┐
#> │ groups ┆ nrs ┆ count ┆ random_sum ┆ reversed names │
#> │ ---    ┆ --- ┆ ---   ┆ ---        ┆ ---            │
#> │ str    ┆ f64 ┆ u32   ┆ f64        ┆ list[str]      │
#> ╞════════╪═════╪═══════╪════════════╪════════════════╡
#> │ C      ┆ 0.0 ┆ 1     ┆ 0.734675   ┆ ["egg"]        │
#> │ A      ┆ 3.0 ┆ 2     ┆ 1.64609    ┆ ["ham", "foo"] │
#> │ B      ┆ 8.0 ┆ 2     ┆ 0.574689   ┆ [null, "spam"] │
#> └────────┴─────┴───────┴────────────┴────────────────┘
```

## GroupBy

``` r
url = "https://theunitedstates.io/congress-legislators/legislators-historical.csv"

dtypes = list(
    "first_name" = pl$Categorical,
    "gender" = pl$Categorical,
    "type" = pl$Categorical,
    "state" = pl$Categorical,
    "party" = pl$Categorical
)

# dtypes argument
dataset = pl$read_csv(url)$with_columns(pl$col("birthday")$str$strptime(pl$Date, "%Y-%m-%d"))
#> tmp file placed in 
#>  /tmp/RtmpVqjWll/https...theunitedstates.io.congress.legislators.legislators.historical.csv

dataset$
  lazy()$
  group_by("first_name")$
  agg(
    pl$count(),
    pl$col("gender"),
    pl$first("last_name"))$
  sort("count", descending = TRUE)$
  limit(5)$
  collect()
#> shape: (5, 4)
#> ┌────────────┬───────┬───────────────────┬───────────┐
#> │ first_name ┆ count ┆ gender            ┆ last_name │
#> │ ---        ┆ ---   ┆ ---               ┆ ---       │
#> │ str        ┆ u32   ┆ list[str]         ┆ str       │
#> ╞════════════╪═══════╪═══════════════════╪═══════════╡
#> │ John       ┆ 1256  ┆ ["M", "M", … "M"] ┆ Walker    │
#> │ William    ┆ 1022  ┆ ["M", "M", … "M"] ┆ Few       │
#> │ James      ┆ 714   ┆ ["M", "M", … "M"] ┆ Armstrong │
#> │ Thomas     ┆ 454   ┆ ["M", "M", … "M"] ┆ Tucker    │
#> │ Charles    ┆ 439   ┆ ["M", "M", … "M"] ┆ Carroll   │
#> └────────────┴───────┴───────────────────┴───────────┘

dataset$lazy()$
  group_by("state")$
  agg(
    (pl$col("party") == "Anti-Administration")$sum()$alias("anti"),
    (pl$col("party") == "Pro-Administration")$sum()$alias("pro"))$
  sort("pro", descending = TRUE)$
  limit(5)$
  collect()
#> shape: (5, 3)
#> ┌───────┬──────┬─────┐
#> │ state ┆ anti ┆ pro │
#> │ ---   ┆ ---  ┆ --- │
#> │ str   ┆ u32  ┆ u32 │
#> ╞═══════╪══════╪═════╡
#> │ NJ    ┆ 0    ┆ 3   │
#> │ CT    ┆ 0    ┆ 3   │
#> │ NC    ┆ 1    ┆ 2   │
#> │ SC    ┆ 0    ┆ 1   │
#> │ MA    ┆ 0    ┆ 1   │
#> └───────┴──────┴─────┘

dataset$
  lazy()$
  group_by(c("state", "party"))$
  agg(pl$count("party")$alias("count"))$
  filter((pl$col("party") == "Anti-Administration") | (pl$col("party") == "Pro-Administration"))$
  sort("count", descending = TRUE)$
  head(5)$
  collect()
#> shape: (5, 3)
#> ┌───────┬─────────────────────┬───────┐
#> │ state ┆ party               ┆ count │
#> │ ---   ┆ ---                 ┆ ---   │
#> │ str   ┆ str                 ┆ u32   │
#> ╞═══════╪═════════════════════╪═══════╡
#> │ CT    ┆ Pro-Administration  ┆ 3     │
#> │ VA    ┆ Anti-Administration ┆ 3     │
#> │ NJ    ┆ Pro-Administration  ┆ 3     │
#> │ NC    ┆ Pro-Administration  ┆ 2     │
#> │ GA    ┆ Anti-Administration ┆ 1     │
#> └───────┴─────────────────────┴───────┘
```

## Folds

## Window functions

``` r
df = pl$read_csv(
  "https://gist.githubusercontent.com/ritchie46/cac6b337ea52281aa23c049250a4ff03/raw/89a957ff3919d90e6ef2d34235e6bf22304f3366/pokemon.csv"
)
```

``` r
filtered = df$
  filter(pl$col("Type 2") == "Psychic")$
  select(c("Name", "Type 1", "Speed"))
filtered
#> shape: (7, 3)
#> ┌─────────────────────┬────────┬───────┐
#> │ Name                ┆ Type 1 ┆ Speed │
#> │ ---                 ┆ ---    ┆ ---   │
#> │ str                 ┆ str    ┆ i64   │
#> ╞═════════════════════╪════════╪═══════╡
#> │ Slowpoke            ┆ Water  ┆ 15    │
#> │ Slowbro             ┆ Water  ┆ 30    │
#> │ SlowbroMega Slowbro ┆ Water  ┆ 30    │
#> │ Exeggcute           ┆ Grass  ┆ 40    │
#> │ Exeggutor           ┆ Grass  ┆ 55    │
#> │ Starmie             ┆ Water  ┆ 115   │
#> │ Jynx                ┆ Ice    ┆ 95    │
#> └─────────────────────┴────────┴───────┘

filtered$with_columns(
  pl$col(c("Name", "Speed"))$sort()$over("Type 1")
)
#> shape: (7, 3)
#> ┌─────────────────────┬────────┬───────┐
#> │ Name                ┆ Type 1 ┆ Speed │
#> │ ---                 ┆ ---    ┆ ---   │
#> │ str                 ┆ str    ┆ i64   │
#> ╞═════════════════════╪════════╪═══════╡
#> │ Slowbro             ┆ Water  ┆ 15    │
#> │ SlowbroMega Slowbro ┆ Water  ┆ 30    │
#> │ Slowpoke            ┆ Water  ┆ 30    │
#> │ Exeggcute           ┆ Grass  ┆ 40    │
#> │ Exeggutor           ┆ Grass  ┆ 55    │
#> │ Starmie             ┆ Water  ┆ 115   │
#> │ Jynx                ┆ Ice    ┆ 95    │
#> └─────────────────────┴────────┴───────┘

# aggregate and broadcast within a group
# output type: -> Int32
pl$sum("foo")$over("groups")
#> polars Expr: col("foo").sum().over([col("groups")])

# sum within a group and multiply with group elements
# output type: -> Int32
(pl$col("x")$sum() * pl$col("y"))$over("groups")
#> polars Expr: [(col("x").sum()) * (col("y"))].over([col("groups")])

# sum within a group and multiply with group elements 
# and aggregate/implode the group to a list
# output type: -> List(Int32)
(pl$col("x")$sum() * pl$col("y"))$implode()$over("groups")
#> polars Expr: [(col("x").sum()) * (col("y"))].list().over([col("groups")])

# note that it will require an explicit `implode()` call
# sum within a group and multiply with group elements 
# and aggregate/implode the group to a list
# the explode call unpack the list and combine inner elements to one column

# This is the fastest method to do things over groups when the groups are sorted
(pl$col("x")$sum() * pl$col("y"))$implode()$over("groups")$explode()
#> polars Expr: [(col("x").sum()) * (col("y"))].list().over([col("groups")]).explode()

df$sort("Type 1")$select(
  pl$col("Type 1")$head(3)$implode()$over("Type 1")$explode(),
  pl$col("Name")$sort_by(pl$col("Speed"))$head(3)$implode()$over("Type 1")$explode()$alias("fastest/group"),
  pl$col("Name")$sort_by(pl$col("Attack"))$head(3)$implode()$over("Type 1")$explode()$alias("strongest/group"),
  pl$col("Name")$sort()$head(3)$implode()$over("Type 1")$explode()$alias("sorted_by_alphabet")
)
#> shape: (43, 4)
#> ┌────────┬─────────────────────┬─────────────────┬─────────────────────────┐
#> │ Type 1 ┆ fastest/group       ┆ strongest/group ┆ sorted_by_alphabet      │
#> │ ---    ┆ ---                 ┆ ---             ┆ ---                     │
#> │ str    ┆ str                 ┆ str             ┆ str                     │
#> ╞════════╪═════════════════════╪═════════════════╪═════════════════════════╡
#> │ Bug    ┆ Paras               ┆ Metapod         ┆ Beedrill                │
#> │ Bug    ┆ Metapod             ┆ Kakuna          ┆ BeedrillMega Beedrill   │
#> │ Bug    ┆ Parasect            ┆ Caterpie        ┆ Butterfree              │
#> │ Dragon ┆ Dratini             ┆ Dratini         ┆ Dragonair               │
#> │ …      ┆ …                   ┆ …               ┆ …                       │
#> │ Rock   ┆ Omanyte             ┆ Omastar         ┆ Geodude                 │
#> │ Water  ┆ Slowpoke            ┆ Magikarp        ┆ Blastoise               │
#> │ Water  ┆ Slowbro             ┆ Tentacool       ┆ BlastoiseMega Blastoise │
#> │ Water  ┆ SlowbroMega Slowbro ┆ Horsea          ┆ Cloyster                │
#> └────────┴─────────────────────┴─────────────────┴─────────────────────────┘
```

# List context and row wise computations

# R examples

``` r
df = pl$DataFrame(
  "A" = c(1, 2, 3, 4, 5),
  "fruits" = c("banana", "banana", "apple", "apple", "banana"),
  "B" = c(5, 4, 3, 2, 1),
  "cars" = c("beetle", "audi", "beetle", "beetle", "beetle"),
  "optional" = c(28, 300, NA, 2, -30)
)
df
#> shape: (5, 5)
#> ┌─────┬────────┬─────┬────────┬──────────┐
#> │ A   ┆ fruits ┆ B   ┆ cars   ┆ optional │
#> │ --- ┆ ---    ┆ --- ┆ ---    ┆ ---      │
#> │ f64 ┆ str    ┆ f64 ┆ str    ┆ f64      │
#> ╞═════╪════════╪═════╪════════╪══════════╡
#> │ 1.0 ┆ banana ┆ 5.0 ┆ beetle ┆ 28.0     │
#> │ 2.0 ┆ banana ┆ 4.0 ┆ audi   ┆ 300.0    │
#> │ 3.0 ┆ apple  ┆ 3.0 ┆ beetle ┆ null     │
#> │ 4.0 ┆ apple  ┆ 2.0 ┆ beetle ┆ 2.0      │
#> │ 5.0 ┆ banana ┆ 1.0 ┆ beetle ┆ -30.0    │
#> └─────┴────────┴─────┴────────┴──────────┘

# Within select, we can use the col function to refer to columns$
# If we are not applying any function to the column, we can also use the column name as a string$
df$select(
  pl$col("A"),
  "B",         # the col part is inferred
  pl$lit("B")  # the pl$lit functions tell polars we mean the literal "B"
)
#> shape: (5, 3)
#> ┌─────┬─────┬─────────┐
#> │ A   ┆ B   ┆ literal │
#> │ --- ┆ --- ┆ ---     │
#> │ f64 ┆ f64 ┆ str     │
#> ╞═════╪═════╪═════════╡
#> │ 1.0 ┆ 5.0 ┆ B       │
#> │ 2.0 ┆ 4.0 ┆ B       │
#> │ 3.0 ┆ 3.0 ┆ B       │
#> │ 4.0 ┆ 2.0 ┆ B       │
#> │ 5.0 ┆ 1.0 ┆ B       │
#> └─────┴─────┴─────────┘

# We can use a list within select (example above) or a comma-separated list of expressions (this example)$
df$select(
  pl$col("A"),
  "B",      
  pl$lit("B")
)
#> shape: (5, 3)
#> ┌─────┬─────┬─────────┐
#> │ A   ┆ B   ┆ literal │
#> │ --- ┆ --- ┆ ---     │
#> │ f64 ┆ f64 ┆ str     │
#> ╞═════╪═════╪═════════╡
#> │ 1.0 ┆ 5.0 ┆ B       │
#> │ 2.0 ┆ 4.0 ┆ B       │
#> │ 3.0 ┆ 3.0 ┆ B       │
#> │ 4.0 ┆ 2.0 ┆ B       │
#> │ 5.0 ┆ 1.0 ┆ B       │
#> └─────┴─────┴─────────┘

# We can select columns with a regex if the regex starts with '^' and ends with '$'
df$select(    
  pl$col("^A|B$")$sum()
)
#> shape: (1, 2)
#> ┌──────┬──────┐
#> │ A    ┆ B    │
#> │ ---  ┆ ---  │
#> │ f64  ┆ f64  │
#> ╞══════╪══════╡
#> │ 15.0 ┆ 15.0 │
#> └──────┴──────┘

# We can select multiple columns by name
df$select(
  pl$col(c("A", "B"))$sum()
)
#> shape: (1, 2)
#> ┌──────┬──────┐
#> │ A    ┆ B    │
#> │ ---  ┆ ---  │
#> │ f64  ┆ f64  │
#> ╞══════╪══════╡
#> │ 15.0 ┆ 15.0 │
#> └──────┴──────┘

# We select everything in normal order
# Then we select everything in reversed order
df$select(
  pl$all(),
  pl$all()$reverse()$name$suffix("_reverse")
)
#> shape: (5, 10)
#> ┌─────┬────────┬─────┬────────┬───┬────────────────┬───────────┬──────────────┬──────────────────┐
#> │ A   ┆ fruits ┆ B   ┆ cars   ┆ … ┆ fruits_reverse ┆ B_reverse ┆ cars_reverse ┆ optional_reverse │
#> │ --- ┆ ---    ┆ --- ┆ ---    ┆   ┆ ---            ┆ ---       ┆ ---          ┆ ---              │
#> │ f64 ┆ str    ┆ f64 ┆ str    ┆   ┆ str            ┆ f64       ┆ str          ┆ f64              │
#> ╞═════╪════════╪═════╪════════╪═══╪════════════════╪═══════════╪══════════════╪══════════════════╡
#> │ 1.0 ┆ banana ┆ 5.0 ┆ beetle ┆ … ┆ banana         ┆ 1.0       ┆ beetle       ┆ -30.0            │
#> │ 2.0 ┆ banana ┆ 4.0 ┆ audi   ┆ … ┆ apple          ┆ 2.0       ┆ beetle       ┆ 2.0              │
#> │ 3.0 ┆ apple  ┆ 3.0 ┆ beetle ┆ … ┆ apple          ┆ 3.0       ┆ beetle       ┆ null             │
#> │ 4.0 ┆ apple  ┆ 2.0 ┆ beetle ┆ … ┆ banana         ┆ 4.0       ┆ audi         ┆ 300.0            │
#> │ 5.0 ┆ banana ┆ 1.0 ┆ beetle ┆ … ┆ banana         ┆ 5.0       ┆ beetle       ┆ 28.0             │
#> └─────┴────────┴─────┴────────┴───┴────────────────┴───────────┴──────────────┴──────────────────┘

# All expressions run in parallel
# Single valued `Series` are broadcasted to the shape of the `DataFrame`
df$select(
  pl$all(),
  pl$all()$sum()$name$suffix("_sum") # This is a single valued Series broadcasted to the shape of the DataFrame
)
#> shape: (5, 10)
#> ┌─────┬────────┬─────┬────────┬───┬────────────┬───────┬──────────┬──────────────┐
#> │ A   ┆ fruits ┆ B   ┆ cars   ┆ … ┆ fruits_sum ┆ B_sum ┆ cars_sum ┆ optional_sum │
#> │ --- ┆ ---    ┆ --- ┆ ---    ┆   ┆ ---        ┆ ---   ┆ ---      ┆ ---          │
#> │ f64 ┆ str    ┆ f64 ┆ str    ┆   ┆ str        ┆ f64   ┆ str      ┆ f64          │
#> ╞═════╪════════╪═════╪════════╪═══╪════════════╪═══════╪══════════╪══════════════╡
#> │ 1.0 ┆ banana ┆ 5.0 ┆ beetle ┆ … ┆ null       ┆ 15.0  ┆ null     ┆ 300.0        │
#> │ 2.0 ┆ banana ┆ 4.0 ┆ audi   ┆ … ┆ null       ┆ 15.0  ┆ null     ┆ 300.0        │
#> │ 3.0 ┆ apple  ┆ 3.0 ┆ beetle ┆ … ┆ null       ┆ 15.0  ┆ null     ┆ 300.0        │
#> │ 4.0 ┆ apple  ┆ 2.0 ┆ beetle ┆ … ┆ null       ┆ 15.0  ┆ null     ┆ 300.0        │
#> │ 5.0 ┆ banana ┆ 1.0 ┆ beetle ┆ … ┆ null       ┆ 15.0  ┆ null     ┆ 300.0        │
#> └─────┴────────┴─────┴────────┴───┴────────────┴───────┴──────────┴──────────────┘

# Filters can also be applied within an expression
df$select(
  # Sum the values of A where the fruits column starts with 'b'
  pl$col("A")$filter(pl$col("fruits")$str$contains("^b$*"))$sum()
)
#> shape: (1, 1)
#> ┌─────┐
#> │ A   │
#> │ --- │
#> │ f64 │
#> ╞═════╡
#> │ 8.0 │
#> └─────┘

# We can do arithmetic on columns
df$select(
  ((pl$col("A") / 124.0 * pl$col("B")) / pl$sum("B"))$alias("computed")
)
#> shape: (5, 1)
#> ┌──────────┐
#> │ computed │
#> │ ---      │
#> │ f64      │
#> ╞══════════╡
#> │ 0.002688 │
#> │ 0.004301 │
#> │ 0.004839 │
#> │ 0.004301 │
#> │ 0.002688 │
#> └──────────┘

# We can combine columns by a predicate
# For example when the `fruits` column is 'banana' we set the value equal to the
# value in `B` column for that row, otherwise we set the value to be -1
df$select(
  "fruits",
  "B",
  pl$when(pl$col("fruits") == "banana")$then(pl$col("B"))$otherwise(-1)$alias("b")
)
#> shape: (5, 3)
#> ┌────────┬─────┬──────┐
#> │ fruits ┆ B   ┆ b    │
#> │ ---    ┆ --- ┆ ---  │
#> │ str    ┆ f64 ┆ f64  │
#> ╞════════╪═════╪══════╡
#> │ banana ┆ 5.0 ┆ 5.0  │
#> │ banana ┆ 4.0 ┆ 4.0  │
#> │ apple  ┆ 3.0 ┆ -1.0 │
#> │ apple  ┆ 2.0 ┆ -1.0 │
#> │ banana ┆ 1.0 ┆ 1.0  │
#> └────────┴─────┴──────┘

# We can combine columns by a fold operation on column level$
# For example we do a horizontal sum where we:
# - start with 0
# - add the value in the `A` column
# - add the value in the `B` column
# - add the value in the `B` column squared
# df$select(
#   "A",
#   "B",
#   pl$fold(0, function(a, b) a + b, c( pl$col("A"), "B", pl$col("B")**2,))$alias("fold")
# )

df$group_by("fruits")$
  agg(
    pl$col("B")$count()$alias("B_count"),
    pl$col("B")$sum()$alias("B_sum")
  )
#> shape: (2, 3)
#> ┌────────┬─────────┬───────┐
#> │ fruits ┆ B_count ┆ B_sum │
#> │ ---    ┆ ---     ┆ ---   │
#> │ str    ┆ u32     ┆ f64   │
#> ╞════════╪═════════╪═══════╡
#> │ banana ┆ 3       ┆ 10.0  │
#> │ apple  ┆ 2       ┆ 5.0   │
#> └────────┴─────────┴───────┘

# We can aggregate many expressions at once
df$group_by("fruits")$
  agg(
            pl$col("B")$sum()$alias("B_sum"),# Sum of B
            # pl$first("fruits")$alias("fruits_first"),# First value of fruits
            # pl$count("A")$alias("count"),# Count of A
            pl$col("cars")$reverse() # Reverse the cars column - not an aggregation
            # so the output is a pl$List
  )
#> shape: (2, 3)
#> ┌────────┬───────┬──────────────────────────────┐
#> │ fruits ┆ B_sum ┆ cars                         │
#> │ ---    ┆ ---   ┆ ---                          │
#> │ str    ┆ f64   ┆ list[str]                    │
#> ╞════════╪═══════╪══════════════════════════════╡
#> │ banana ┆ 10.0  ┆ ["beetle", "audi", "beetle"] │
#> │ apple  ┆ 5.0   ┆ ["beetle", "beetle"]         │
#> └────────┴───────┴──────────────────────────────┘
```

``` r
# We can also get a list of the row indices for each group with `agg_groups()`
df$
  group_by("fruits")$
  agg(pl$col("B")$agg_groups()$alias("group_row_indices"))
#> shape: (2, 2)
#> ┌────────┬───────────────────┐
#> │ fruits ┆ group_row_indices │
#> │ ---    ┆ ---               │
#> │ str    ┆ list[u32]         │
#> ╞════════╪═══════════════════╡
#> │ banana ┆ [0, 1, 4]         │
#> │ apple  ┆ [2, 3]            │
#> └────────┴───────────────────┘

# We can also do filter predicates in group_by
# In this example we do not include values of B that are smaller than 1
# in the sum
df$
  group_by("fruits")$
  agg(pl$col("B")$filter(pl$col("B") > 1)$sum())
#> shape: (2, 2)
#> ┌────────┬─────┐
#> │ fruits ┆ B   │
#> │ ---    ┆ --- │
#> │ str    ┆ f64 │
#> ╞════════╪═════╡
#> │ apple  ┆ 5.0 │
#> │ banana ┆ 9.0 │
#> └────────┴─────┘


# Here we add a new column with the sum of B grouped by fruits
df$
  select(
    "fruits",
    "cars",
    "B",
    pl$col("B")$sum()$over("fruits")$alias("B_sum_by_fruits"))
#> shape: (5, 4)
#> ┌────────┬────────┬─────┬─────────────────┐
#> │ fruits ┆ cars   ┆ B   ┆ B_sum_by_fruits │
#> │ ---    ┆ ---    ┆ --- ┆ ---             │
#> │ str    ┆ str    ┆ f64 ┆ f64             │
#> ╞════════╪════════╪═════╪═════════════════╡
#> │ banana ┆ beetle ┆ 5.0 ┆ 10.0            │
#> │ banana ┆ audi   ┆ 4.0 ┆ 10.0            │
#> │ apple  ┆ beetle ┆ 3.0 ┆ 5.0             │
#> │ apple  ┆ beetle ┆ 2.0 ┆ 5.0             │
#> │ banana ┆ beetle ┆ 1.0 ┆ 10.0            │
#> └────────┴────────┴─────┴─────────────────┘

# We can also use window functions to do group_by over multiple columns
df$
  select(
    "fruits",
    "cars",
    "B",
    pl$col("B")$sum()$over("fruits")$alias("B_sum_by_fruits"),
    pl$col("B")$sum()$over("cars")$alias("B_sum_by_cars"))
#> shape: (5, 5)
#> ┌────────┬────────┬─────┬─────────────────┬───────────────┐
#> │ fruits ┆ cars   ┆ B   ┆ B_sum_by_fruits ┆ B_sum_by_cars │
#> │ ---    ┆ ---    ┆ --- ┆ ---             ┆ ---           │
#> │ str    ┆ str    ┆ f64 ┆ f64             ┆ f64           │
#> ╞════════╪════════╪═════╪═════════════════╪═══════════════╡
#> │ banana ┆ beetle ┆ 5.0 ┆ 10.0            ┆ 11.0          │
#> │ banana ┆ audi   ┆ 4.0 ┆ 10.0            ┆ 4.0           │
#> │ apple  ┆ beetle ┆ 3.0 ┆ 5.0             ┆ 11.0          │
#> │ apple  ┆ beetle ┆ 2.0 ┆ 5.0             ┆ 11.0          │
#> │ banana ┆ beetle ┆ 1.0 ┆ 10.0            ┆ 11.0          │
#> └────────┴────────┴─────┴─────────────────┴───────────────┘

# Here we use a window function to lag column B within "fruits"
df$
  select(
    "fruits",
    "B",
    pl$col("B")$shift()$over("fruits")$alias("lag_B_by_fruits"))
#> shape: (5, 3)
#> ┌────────┬─────┬─────────────────┐
#> │ fruits ┆ B   ┆ lag_B_by_fruits │
#> │ ---    ┆ --- ┆ ---             │
#> │ str    ┆ f64 ┆ f64             │
#> ╞════════╪═════╪═════════════════╡
#> │ banana ┆ 5.0 ┆ null            │
#> │ banana ┆ 4.0 ┆ 5.0             │
#> │ apple  ┆ 3.0 ┆ null            │
#> │ apple  ┆ 2.0 ┆ 3.0             │
#> │ banana ┆ 1.0 ┆ 4.0             │
#> └────────┴─────┴─────────────────┘
```
