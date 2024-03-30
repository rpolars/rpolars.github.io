

# Filter rows of a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L884)

## Description

Filter rows with an Expression defining a boolean column. Multiple
expressions are combined with <code>&</code> (AND). This is equivalent
to <code>dplyr::filter()</code>.

## Usage

<pre><code class='language-R'>DataFrame_filter(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_filter_:_...">…</code>
</td>
<td>
Polars expressions which will evaluate to a boolean.
</td>
</tr>
</table>

## Details

Rows where the condition returns <code>NA</code> are dropped.

## Value

A DataFrame with only the rows where the conditions are
<code>TRUE</code>.

## Examples

``` r
library(polars)

df = pl$DataFrame(iris)

df$filter(pl$col("Sepal.Length") > 5)
```

    #> shape: (118, 5)
    #> ┌──────────────┬─────────────┬──────────────┬─────────────┬───────────┐
    #> │ Sepal.Length ┆ Sepal.Width ┆ Petal.Length ┆ Petal.Width ┆ Species   │
    #> │ ---          ┆ ---         ┆ ---          ┆ ---         ┆ ---       │
    #> │ f64          ┆ f64         ┆ f64          ┆ f64         ┆ cat       │
    #> ╞══════════════╪═════════════╪══════════════╪═════════════╪═══════════╡
    #> │ 5.1          ┆ 3.5         ┆ 1.4          ┆ 0.2         ┆ setosa    │
    #> │ 5.4          ┆ 3.9         ┆ 1.7          ┆ 0.4         ┆ setosa    │
    #> │ 5.4          ┆ 3.7         ┆ 1.5          ┆ 0.2         ┆ setosa    │
    #> │ 5.8          ┆ 4.0         ┆ 1.2          ┆ 0.2         ┆ setosa    │
    #> │ 5.7          ┆ 4.4         ┆ 1.5          ┆ 0.4         ┆ setosa    │
    #> │ …            ┆ …           ┆ …            ┆ …           ┆ …         │
    #> │ 6.7          ┆ 3.0         ┆ 5.2          ┆ 2.3         ┆ virginica │
    #> │ 6.3          ┆ 2.5         ┆ 5.0          ┆ 1.9         ┆ virginica │
    #> │ 6.5          ┆ 3.0         ┆ 5.2          ┆ 2.0         ┆ virginica │
    #> │ 6.2          ┆ 3.4         ┆ 5.4          ┆ 2.3         ┆ virginica │
    #> │ 5.9          ┆ 3.0         ┆ 5.1          ┆ 1.8         ┆ virginica │
    #> └──────────────┴─────────────┴──────────────┴─────────────┴───────────┘

``` r
# This is equivalent to
# df$filter(pl$col("Sepal.Length") > 5 & pl$col("Petal.Width") < 1)
df$filter(pl$col("Sepal.Length") > 5, pl$col("Petal.Width") < 1)
```

    #> shape: (22, 5)
    #> ┌──────────────┬─────────────┬──────────────┬─────────────┬─────────┐
    #> │ Sepal.Length ┆ Sepal.Width ┆ Petal.Length ┆ Petal.Width ┆ Species │
    #> │ ---          ┆ ---         ┆ ---          ┆ ---         ┆ ---     │
    #> │ f64          ┆ f64         ┆ f64          ┆ f64         ┆ cat     │
    #> ╞══════════════╪═════════════╪══════════════╪═════════════╪═════════╡
    #> │ 5.1          ┆ 3.5         ┆ 1.4          ┆ 0.2         ┆ setosa  │
    #> │ 5.4          ┆ 3.9         ┆ 1.7          ┆ 0.4         ┆ setosa  │
    #> │ 5.4          ┆ 3.7         ┆ 1.5          ┆ 0.2         ┆ setosa  │
    #> │ 5.8          ┆ 4.0         ┆ 1.2          ┆ 0.2         ┆ setosa  │
    #> │ 5.7          ┆ 4.4         ┆ 1.5          ┆ 0.4         ┆ setosa  │
    #> │ …            ┆ …           ┆ …            ┆ …           ┆ …       │
    #> │ 5.5          ┆ 3.5         ┆ 1.3          ┆ 0.2         ┆ setosa  │
    #> │ 5.1          ┆ 3.4         ┆ 1.5          ┆ 0.2         ┆ setosa  │
    #> │ 5.1          ┆ 3.8         ┆ 1.9          ┆ 0.4         ┆ setosa  │
    #> │ 5.1          ┆ 3.8         ┆ 1.6          ┆ 0.2         ┆ setosa  │
    #> │ 5.3          ┆ 3.7         ┆ 1.5          ┆ 0.2         ┆ setosa  │
    #> └──────────────┴─────────────┴──────────────┴─────────────┴─────────┘

``` r
# rows where condition is NA are dropped
iris2 = iris
iris2[c(1, 3, 5), "Species"] = NA
df = pl$DataFrame(iris2)

df$filter(pl$col("Species") == "setosa")
```

    #> shape: (47, 5)
    #> ┌──────────────┬─────────────┬──────────────┬─────────────┬─────────┐
    #> │ Sepal.Length ┆ Sepal.Width ┆ Petal.Length ┆ Petal.Width ┆ Species │
    #> │ ---          ┆ ---         ┆ ---          ┆ ---         ┆ ---     │
    #> │ f64          ┆ f64         ┆ f64          ┆ f64         ┆ cat     │
    #> ╞══════════════╪═════════════╪══════════════╪═════════════╪═════════╡
    #> │ 4.9          ┆ 3.0         ┆ 1.4          ┆ 0.2         ┆ setosa  │
    #> │ 4.6          ┆ 3.1         ┆ 1.5          ┆ 0.2         ┆ setosa  │
    #> │ 5.4          ┆ 3.9         ┆ 1.7          ┆ 0.4         ┆ setosa  │
    #> │ 4.6          ┆ 3.4         ┆ 1.4          ┆ 0.3         ┆ setosa  │
    #> │ 5.0          ┆ 3.4         ┆ 1.5          ┆ 0.2         ┆ setosa  │
    #> │ …            ┆ …           ┆ …            ┆ …           ┆ …       │
    #> │ 4.8          ┆ 3.0         ┆ 1.4          ┆ 0.3         ┆ setosa  │
    #> │ 5.1          ┆ 3.8         ┆ 1.6          ┆ 0.2         ┆ setosa  │
    #> │ 4.6          ┆ 3.2         ┆ 1.4          ┆ 0.2         ┆ setosa  │
    #> │ 5.3          ┆ 3.7         ┆ 1.5          ┆ 0.2         ┆ setosa  │
    #> │ 5.0          ┆ 3.3         ┆ 1.4          ┆ 0.2         ┆ setosa  │
    #> └──────────────┴─────────────┴──────────────┴─────────────┴─────────┘
