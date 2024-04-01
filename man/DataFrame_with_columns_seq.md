

# Modify/append column(s)

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L872)

## Description

Add columns or modify existing ones with expressions. This is the
equivalent of <code>dplyr::mutate()</code> as it keeps unmentioned
columns (unlike <code style="white-space: pre;">$select()</code>).

This will run all expression sequentially instead of in parallel. Use
this when the work per expression is cheap. Otherwise,
<code style="white-space: pre;">$with_columns()</code> should be
preferred.

## Usage

<pre><code class='language-R'>DataFrame_with_columns_seq(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_with_columns_seq_:_...">…</code>
</td>
<td>
Any expressions or string column name, or same wrapped in a list. If
first and only element is a list, it is unwrapped as a list of args.
</td>
</tr>
</table>

## Value

A DataFrame

## Examples

``` r
library(polars)

pl$DataFrame(iris)$with_columns_seq(
  pl$col("Sepal.Length")$abs()$alias("abs_SL"),
  (pl$col("Sepal.Length") + 2)$alias("add_2_SL")
)
```

    #> shape: (150, 7)
    #> ┌──────────────┬─────────────┬──────────────┬─────────────┬───────────┬────────┬──────────┐
    #> │ Sepal.Length ┆ Sepal.Width ┆ Petal.Length ┆ Petal.Width ┆ Species   ┆ abs_SL ┆ add_2_SL │
    #> │ ---          ┆ ---         ┆ ---          ┆ ---         ┆ ---       ┆ ---    ┆ ---      │
    #> │ f64          ┆ f64         ┆ f64          ┆ f64         ┆ cat       ┆ f64    ┆ f64      │
    #> ╞══════════════╪═════════════╪══════════════╪═════════════╪═══════════╪════════╪══════════╡
    #> │ 5.1          ┆ 3.5         ┆ 1.4          ┆ 0.2         ┆ setosa    ┆ 5.1    ┆ 7.1      │
    #> │ 4.9          ┆ 3.0         ┆ 1.4          ┆ 0.2         ┆ setosa    ┆ 4.9    ┆ 6.9      │
    #> │ 4.7          ┆ 3.2         ┆ 1.3          ┆ 0.2         ┆ setosa    ┆ 4.7    ┆ 6.7      │
    #> │ 4.6          ┆ 3.1         ┆ 1.5          ┆ 0.2         ┆ setosa    ┆ 4.6    ┆ 6.6      │
    #> │ 5.0          ┆ 3.6         ┆ 1.4          ┆ 0.2         ┆ setosa    ┆ 5.0    ┆ 7.0      │
    #> │ …            ┆ …           ┆ …            ┆ …           ┆ …         ┆ …      ┆ …        │
    #> │ 6.7          ┆ 3.0         ┆ 5.2          ┆ 2.3         ┆ virginica ┆ 6.7    ┆ 8.7      │
    #> │ 6.3          ┆ 2.5         ┆ 5.0          ┆ 1.9         ┆ virginica ┆ 6.3    ┆ 8.3      │
    #> │ 6.5          ┆ 3.0         ┆ 5.2          ┆ 2.0         ┆ virginica ┆ 6.5    ┆ 8.5      │
    #> │ 6.2          ┆ 3.4         ┆ 5.4          ┆ 2.3         ┆ virginica ┆ 6.2    ┆ 8.2      │
    #> │ 5.9          ┆ 3.0         ┆ 5.1          ┆ 1.8         ┆ virginica ┆ 5.9    ┆ 7.9      │
    #> └──────────────┴─────────────┴──────────────┴─────────────┴───────────┴────────┴──────────┘

``` r
# same query
l_expr = list(
  pl$col("Sepal.Length")$abs()$alias("abs_SL"),
  (pl$col("Sepal.Length") + 2)$alias("add_2_SL")
)
pl$DataFrame(iris)$with_columns_seq(l_expr)
```

    #> shape: (150, 7)
    #> ┌──────────────┬─────────────┬──────────────┬─────────────┬───────────┬────────┬──────────┐
    #> │ Sepal.Length ┆ Sepal.Width ┆ Petal.Length ┆ Petal.Width ┆ Species   ┆ abs_SL ┆ add_2_SL │
    #> │ ---          ┆ ---         ┆ ---          ┆ ---         ┆ ---       ┆ ---    ┆ ---      │
    #> │ f64          ┆ f64         ┆ f64          ┆ f64         ┆ cat       ┆ f64    ┆ f64      │
    #> ╞══════════════╪═════════════╪══════════════╪═════════════╪═══════════╪════════╪══════════╡
    #> │ 5.1          ┆ 3.5         ┆ 1.4          ┆ 0.2         ┆ setosa    ┆ 5.1    ┆ 7.1      │
    #> │ 4.9          ┆ 3.0         ┆ 1.4          ┆ 0.2         ┆ setosa    ┆ 4.9    ┆ 6.9      │
    #> │ 4.7          ┆ 3.2         ┆ 1.3          ┆ 0.2         ┆ setosa    ┆ 4.7    ┆ 6.7      │
    #> │ 4.6          ┆ 3.1         ┆ 1.5          ┆ 0.2         ┆ setosa    ┆ 4.6    ┆ 6.6      │
    #> │ 5.0          ┆ 3.6         ┆ 1.4          ┆ 0.2         ┆ setosa    ┆ 5.0    ┆ 7.0      │
    #> │ …            ┆ …           ┆ …            ┆ …           ┆ …         ┆ …      ┆ …        │
    #> │ 6.7          ┆ 3.0         ┆ 5.2          ┆ 2.3         ┆ virginica ┆ 6.7    ┆ 8.7      │
    #> │ 6.3          ┆ 2.5         ┆ 5.0          ┆ 1.9         ┆ virginica ┆ 6.3    ┆ 8.3      │
    #> │ 6.5          ┆ 3.0         ┆ 5.2          ┆ 2.0         ┆ virginica ┆ 6.5    ┆ 8.5      │
    #> │ 6.2          ┆ 3.4         ┆ 5.4          ┆ 2.3         ┆ virginica ┆ 6.2    ┆ 8.2      │
    #> │ 5.9          ┆ 3.0         ┆ 5.1          ┆ 1.8         ┆ virginica ┆ 5.9    ┆ 7.9      │
    #> └──────────────┴─────────────┴──────────────┴─────────────┴───────────┴────────┴──────────┘

``` r
pl$DataFrame(iris)$with_columns_seq(
  pl$col("Sepal.Length")$abs(), # not named expr will keep name "Sepal.Length"
  SW_add_2 = (pl$col("Sepal.Width") + 2)
)
```

    #> shape: (150, 6)
    #> ┌──────────────┬─────────────┬──────────────┬─────────────┬───────────┬──────────┐
    #> │ Sepal.Length ┆ Sepal.Width ┆ Petal.Length ┆ Petal.Width ┆ Species   ┆ SW_add_2 │
    #> │ ---          ┆ ---         ┆ ---          ┆ ---         ┆ ---       ┆ ---      │
    #> │ f64          ┆ f64         ┆ f64          ┆ f64         ┆ cat       ┆ f64      │
    #> ╞══════════════╪═════════════╪══════════════╪═════════════╪═══════════╪══════════╡
    #> │ 5.1          ┆ 3.5         ┆ 1.4          ┆ 0.2         ┆ setosa    ┆ 5.5      │
    #> │ 4.9          ┆ 3.0         ┆ 1.4          ┆ 0.2         ┆ setosa    ┆ 5.0      │
    #> │ 4.7          ┆ 3.2         ┆ 1.3          ┆ 0.2         ┆ setosa    ┆ 5.2      │
    #> │ 4.6          ┆ 3.1         ┆ 1.5          ┆ 0.2         ┆ setosa    ┆ 5.1      │
    #> │ 5.0          ┆ 3.6         ┆ 1.4          ┆ 0.2         ┆ setosa    ┆ 5.6      │
    #> │ …            ┆ …           ┆ …            ┆ …           ┆ …         ┆ …        │
    #> │ 6.7          ┆ 3.0         ┆ 5.2          ┆ 2.3         ┆ virginica ┆ 5.0      │
    #> │ 6.3          ┆ 2.5         ┆ 5.0          ┆ 1.9         ┆ virginica ┆ 4.5      │
    #> │ 6.5          ┆ 3.0         ┆ 5.2          ┆ 2.0         ┆ virginica ┆ 5.0      │
    #> │ 6.2          ┆ 3.4         ┆ 5.4          ┆ 2.3         ┆ virginica ┆ 5.4      │
    #> │ 5.9          ┆ 3.0         ┆ 5.1          ┆ 1.8         ┆ virginica ┆ 5.0      │
    #> └──────────────┴─────────────┴──────────────┴─────────────┴───────────┴──────────┘
