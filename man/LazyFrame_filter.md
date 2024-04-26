

# Apply filter to LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L378)

## Description

Filter rows with an Expression defining a boolean column. Multiple
expressions are combined with <code>&</code> (AND). This is equivalent
to <code>dplyr::filter()</code>.

## Usage

<pre><code class='language-R'>LazyFrame_filter(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="...">…</code>
</td>
<td>
Polars expressions which will evaluate to a boolean.
</td>
</tr>
</table>

## Details

Rows where the condition returns <code>NA</code> are dropped.

## Value

A new <code>LazyFrame</code> object with add/modified column.

## Examples

``` r
library(polars)

lf = pl$LazyFrame(iris)

lf$filter(pl$col("Species") == "setosa")$collect()
```

    #> shape: (50, 5)
    #> ┌──────────────┬─────────────┬──────────────┬─────────────┬─────────┐
    #> │ Sepal.Length ┆ Sepal.Width ┆ Petal.Length ┆ Petal.Width ┆ Species │
    #> │ ---          ┆ ---         ┆ ---          ┆ ---         ┆ ---     │
    #> │ f64          ┆ f64         ┆ f64          ┆ f64         ┆ cat     │
    #> ╞══════════════╪═════════════╪══════════════╪═════════════╪═════════╡
    #> │ 5.1          ┆ 3.5         ┆ 1.4          ┆ 0.2         ┆ setosa  │
    #> │ 4.9          ┆ 3.0         ┆ 1.4          ┆ 0.2         ┆ setosa  │
    #> │ 4.7          ┆ 3.2         ┆ 1.3          ┆ 0.2         ┆ setosa  │
    #> │ 4.6          ┆ 3.1         ┆ 1.5          ┆ 0.2         ┆ setosa  │
    #> │ 5.0          ┆ 3.6         ┆ 1.4          ┆ 0.2         ┆ setosa  │
    #> │ …            ┆ …           ┆ …            ┆ …           ┆ …       │
    #> │ 4.8          ┆ 3.0         ┆ 1.4          ┆ 0.3         ┆ setosa  │
    #> │ 5.1          ┆ 3.8         ┆ 1.6          ┆ 0.2         ┆ setosa  │
    #> │ 4.6          ┆ 3.2         ┆ 1.4          ┆ 0.2         ┆ setosa  │
    #> │ 5.3          ┆ 3.7         ┆ 1.5          ┆ 0.2         ┆ setosa  │
    #> │ 5.0          ┆ 3.3         ┆ 1.4          ┆ 0.2         ┆ setosa  │
    #> └──────────────┴─────────────┴──────────────┴─────────────┴─────────┘

``` r
# This is equivalent to
# lf$filter(pl$col("Sepal.Length") > 5 & pl$col("Petal.Width") < 1)
lf$filter(pl$col("Sepal.Length") > 5, pl$col("Petal.Width") < 1)
```

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #> FILTER [([(col("Sepal.Length")) > (5.0)]) & ([(col("Petal.Width")) < (1.0)])] FROM
    #> DF ["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]; PROJECT */5 COLUMNS; SELECTION: "None"
