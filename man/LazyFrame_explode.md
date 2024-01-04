
# Explode columns containing a list of values

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L1530)

## Description

This will take every element of a list column and add it on an
additional row.

## Usage

<pre><code class='language-R'>LazyFrame_explode(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_explode_:_...">…</code>
</td>
<td>
Column(s) to be exploded as individual
<code style="white-space: pre;">Into\<Expr\></code> or list/vector of
<code style="white-space: pre;">Into\<Expr\></code>. In a handful of
places in rust-polars, only the plain variant <code>Expr::Column</code>
is accepted. This is currenly one of such places. Therefore
<code>pl$col(“name”)</code> and <code>pl$all()</code> is allowed, not
<code>pl$col(“name”)$alias(“newname”)</code>. <code>“name”</code> is
implicitly converted to <code>pl$col(“name”)</code>.
</td>
</tr>
</table>

## Details

Only columns of DataType <code>List</code> or <code>String</code> can be
exploded.

Named expressions like <code style="white-space: pre;">$explode(a =
pl$col(“b”))</code> will not implicitly trigger
<code style="white-space: pre;">$alias(“a”)</code> here, due to only
variant <code>Expr::Column</code> is supported in rust-polars.

## Value

LazyFrame

## Examples

``` r
library(polars)

df = pl$LazyFrame(
  letters = c("aa", "aa", "bb", "cc"),
  numbers = list(1, c(2, 3), c(4, 5), c(6, 7, 8)),
  numbers_2 = list(0, c(1, 2), c(3, 4), c(5, 6, 7)) # same structure as numbers
)
df
```

    #> [1] "polars LazyFrame naive plan: (run ldf$describe_optimized_plan() to see the optimized plan)"
    #> DF ["letters", "numbers", "numbers_2"]; PROJECT */3 COLUMNS; SELECTION: "None"

``` r
# explode a single column, append others
df$explode("numbers")$collect()
```

    #> shape: (8, 3)
    #> ┌─────────┬─────────┬─────────────────┐
    #> │ letters ┆ numbers ┆ numbers_2       │
    #> │ ---     ┆ ---     ┆ ---             │
    #> │ str     ┆ f64     ┆ list[f64]       │
    #> ╞═════════╪═════════╪═════════════════╡
    #> │ aa      ┆ 1.0     ┆ [0.0]           │
    #> │ aa      ┆ 2.0     ┆ [1.0, 2.0]      │
    #> │ aa      ┆ 3.0     ┆ [1.0, 2.0]      │
    #> │ bb      ┆ 4.0     ┆ [3.0, 4.0]      │
    #> │ bb      ┆ 5.0     ┆ [3.0, 4.0]      │
    #> │ cc      ┆ 6.0     ┆ [5.0, 6.0, 7.0] │
    #> │ cc      ┆ 7.0     ┆ [5.0, 6.0, 7.0] │
    #> │ cc      ┆ 8.0     ┆ [5.0, 6.0, 7.0] │
    #> └─────────┴─────────┴─────────────────┘

``` r
# it is also possible to explode a character column to have one letter per row
df$explode("letters")
```

    #> [1] "polars LazyFrame naive plan: (run ldf$describe_optimized_plan() to see the optimized plan)"
    #> EXPLODE
    #>   DF ["letters", "numbers", "numbers_2"]; PROJECT */3 COLUMNS; SELECTION: "None"

``` r
# explode two columns of same nesting structure, by names or the common dtype
# "List(Float64)"
df$explode("numbers", "numbers_2")$collect()
```

    #> shape: (8, 3)
    #> ┌─────────┬─────────┬───────────┐
    #> │ letters ┆ numbers ┆ numbers_2 │
    #> │ ---     ┆ ---     ┆ ---       │
    #> │ str     ┆ f64     ┆ f64       │
    #> ╞═════════╪═════════╪═══════════╡
    #> │ aa      ┆ 1.0     ┆ 0.0       │
    #> │ aa      ┆ 2.0     ┆ 1.0       │
    #> │ aa      ┆ 3.0     ┆ 2.0       │
    #> │ bb      ┆ 4.0     ┆ 3.0       │
    #> │ bb      ┆ 5.0     ┆ 4.0       │
    #> │ cc      ┆ 6.0     ┆ 5.0       │
    #> │ cc      ┆ 7.0     ┆ 6.0       │
    #> │ cc      ┆ 8.0     ┆ 7.0       │
    #> └─────────┴─────────┴───────────┘

``` r
df$explode(pl$col(pl$List(pl$Float64)))$collect()
```

    #> shape: (8, 3)
    #> ┌─────────┬─────────┬───────────┐
    #> │ letters ┆ numbers ┆ numbers_2 │
    #> │ ---     ┆ ---     ┆ ---       │
    #> │ str     ┆ f64     ┆ f64       │
    #> ╞═════════╪═════════╪═══════════╡
    #> │ aa      ┆ 1.0     ┆ 0.0       │
    #> │ aa      ┆ 2.0     ┆ 1.0       │
    #> │ aa      ┆ 3.0     ┆ 2.0       │
    #> │ bb      ┆ 4.0     ┆ 3.0       │
    #> │ bb      ┆ 5.0     ┆ 4.0       │
    #> │ cc      ┆ 6.0     ┆ 5.0       │
    #> │ cc      ┆ 7.0     ┆ 6.0       │
    #> │ cc      ┆ 8.0     ┆ 7.0       │
    #> └─────────┴─────────┴───────────┘
