
# Exclude certain columns from selection

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/expr__expr.R#L1094)

## Description

Exclude certain columns from selection

## Usage

<pre><code class='language-R'>Expr_exclude(columns)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_exclude_:_columns">columns</code>
</td>
<td>

Given param type:

<ul>
<li>

string: single column name or regex starting with <code>^</code> and
ending with <code>$</code>

</li>
<li>

character vector: exclude all these column names, no regex allowed

</li>
<li>

DataType: Exclude any of this DataType

</li>
<li>

List(DataType): Exclude any of these DataType(s)

</li>
</ul>
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)


# make DataFrame
df = pl$DataFrame(iris)

# by name(s)
df$select(pl$all()$exclude("Species"))
```

    #> shape: (150, 4)
    #> ┌──────────────┬─────────────┬──────────────┬─────────────┐
    #> │ Sepal.Length ┆ Sepal.Width ┆ Petal.Length ┆ Petal.Width │
    #> │ ---          ┆ ---         ┆ ---          ┆ ---         │
    #> │ f64          ┆ f64         ┆ f64          ┆ f64         │
    #> ╞══════════════╪═════════════╪══════════════╪═════════════╡
    #> │ 5.1          ┆ 3.5         ┆ 1.4          ┆ 0.2         │
    #> │ 4.9          ┆ 3.0         ┆ 1.4          ┆ 0.2         │
    #> │ 4.7          ┆ 3.2         ┆ 1.3          ┆ 0.2         │
    #> │ 4.6          ┆ 3.1         ┆ 1.5          ┆ 0.2         │
    #> │ …            ┆ …           ┆ …            ┆ …           │
    #> │ 6.3          ┆ 2.5         ┆ 5.0          ┆ 1.9         │
    #> │ 6.5          ┆ 3.0         ┆ 5.2          ┆ 2.0         │
    #> │ 6.2          ┆ 3.4         ┆ 5.4          ┆ 2.3         │
    #> │ 5.9          ┆ 3.0         ┆ 5.1          ┆ 1.8         │
    #> └──────────────┴─────────────┴──────────────┴─────────────┘

``` r
# by type
df$select(pl$all()$exclude(pl$Categorical))
```

    #> shape: (150, 4)
    #> ┌──────────────┬─────────────┬──────────────┬─────────────┐
    #> │ Sepal.Length ┆ Sepal.Width ┆ Petal.Length ┆ Petal.Width │
    #> │ ---          ┆ ---         ┆ ---          ┆ ---         │
    #> │ f64          ┆ f64         ┆ f64          ┆ f64         │
    #> ╞══════════════╪═════════════╪══════════════╪═════════════╡
    #> │ 5.1          ┆ 3.5         ┆ 1.4          ┆ 0.2         │
    #> │ 4.9          ┆ 3.0         ┆ 1.4          ┆ 0.2         │
    #> │ 4.7          ┆ 3.2         ┆ 1.3          ┆ 0.2         │
    #> │ 4.6          ┆ 3.1         ┆ 1.5          ┆ 0.2         │
    #> │ …            ┆ …           ┆ …            ┆ …           │
    #> │ 6.3          ┆ 2.5         ┆ 5.0          ┆ 1.9         │
    #> │ 6.5          ┆ 3.0         ┆ 5.2          ┆ 2.0         │
    #> │ 6.2          ┆ 3.4         ┆ 5.4          ┆ 2.3         │
    #> │ 5.9          ┆ 3.0         ┆ 5.1          ┆ 1.8         │
    #> └──────────────┴─────────────┴──────────────┴─────────────┘

``` r
df$select(pl$all()$exclude(list(pl$Categorical, pl$Float64)))
```

    #> shape: (0, 0)
    #> ┌┐
    #> ╞╡
    #> └┘

``` r
# by regex
df$select(pl$all()$exclude("^Sepal.*$"))
```

    #> shape: (150, 3)
    #> ┌──────────────┬─────────────┬───────────┐
    #> │ Petal.Length ┆ Petal.Width ┆ Species   │
    #> │ ---          ┆ ---         ┆ ---       │
    #> │ f64          ┆ f64         ┆ cat       │
    #> ╞══════════════╪═════════════╪═══════════╡
    #> │ 1.4          ┆ 0.2         ┆ setosa    │
    #> │ 1.4          ┆ 0.2         ┆ setosa    │
    #> │ 1.3          ┆ 0.2         ┆ setosa    │
    #> │ 1.5          ┆ 0.2         ┆ setosa    │
    #> │ …            ┆ …           ┆ …         │
    #> │ 5.0          ┆ 1.9         ┆ virginica │
    #> │ 5.2          ┆ 2.0         ┆ virginica │
    #> │ 5.4          ┆ 2.3         ┆ virginica │
    #> │ 5.1          ┆ 1.8         ┆ virginica │
    #> └──────────────┴─────────────┴───────────┘
