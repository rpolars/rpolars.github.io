

# Create new DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/dataframe__frame.R#L227)

## Description

Create new DataFrame

## Usage

<pre><code class='language-R'>pl_DataFrame(..., make_names_unique = TRUE, schema = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_DataFrame_:_...">…</code>
</td>
<td>

One of the following:

<ul>
<li>

a data.frame or something that inherits data.frame or DataFrame

</li>
<li>

a list of mixed vectors and Series of equal length

</li>
<li>

mixed vectors and/or Series of equal length

</li>
</ul>
Columns will be named as of named arguments or alternatively by names of
Series or given a placeholder name.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_DataFrame_:_make_names_unique">make_names_unique</code>
</td>
<td>
If <code>TRUE</code> (default), any duplicated names will be prefixed a
running number.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_DataFrame_:_schema">schema</code>
</td>
<td>
A named list that will be used to convert a variable to a specific
DataType. See Examples.
</td>
</tr>
</table>

## Value

DataFrame

## Examples

``` r
library(polars)

pl$DataFrame(
  a = list(c(1, 2, 3, 4, 5)), # NB if first column should be a list, wrap it in a Series
  b = 1:5,
  c = letters[1:5],
  d = list(1:1, 1:2, 1:3, 1:4, 1:5)
) # directly from vectors
```

    #> shape: (5, 4)
    #> ┌───────────────────┬─────┬─────┬─────────────┐
    #> │ a                 ┆ b   ┆ c   ┆ d           │
    #> │ ---               ┆ --- ┆ --- ┆ ---         │
    #> │ list[f64]         ┆ i32 ┆ str ┆ list[i32]   │
    #> ╞═══════════════════╪═════╪═════╪═════════════╡
    #> │ [1.0, 2.0, … 5.0] ┆ 1   ┆ a   ┆ [1]         │
    #> │ [1.0, 2.0, … 5.0] ┆ 2   ┆ b   ┆ [1, 2]      │
    #> │ [1.0, 2.0, … 5.0] ┆ 3   ┆ c   ┆ [1, 2, 3]   │
    #> │ [1.0, 2.0, … 5.0] ┆ 4   ┆ d   ┆ [1, 2, … 4] │
    #> │ [1.0, 2.0, … 5.0] ┆ 5   ┆ e   ┆ [1, 2, … 5] │
    #> └───────────────────┴─────┴─────┴─────────────┘

``` r
# from a list of vectors
pl$DataFrame(list(
  a = c(1, 2, 3, 4, 5),
  b = 1:5,
  c = letters[1:5],
  d = list(1L, 1:2, 1:3, 1:4, 1:5)
))
```

    #> shape: (5, 4)
    #> ┌─────┬─────┬─────┬─────────────┐
    #> │ a   ┆ b   ┆ c   ┆ d           │
    #> │ --- ┆ --- ┆ --- ┆ ---         │
    #> │ f64 ┆ i32 ┆ str ┆ list[i32]   │
    #> ╞═════╪═════╪═════╪═════════════╡
    #> │ 1.0 ┆ 1   ┆ a   ┆ [1]         │
    #> │ 2.0 ┆ 2   ┆ b   ┆ [1, 2]      │
    #> │ 3.0 ┆ 3   ┆ c   ┆ [1, 2, 3]   │
    #> │ 4.0 ┆ 4   ┆ d   ┆ [1, 2, … 4] │
    #> │ 5.0 ┆ 5   ┆ e   ┆ [1, 2, … 5] │
    #> └─────┴─────┴─────┴─────────────┘

``` r
# from a data.frame
pl$DataFrame(mtcars)
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
    #> │ 18.7 ┆ 8.0 ┆ 360.0 ┆ 175.0 ┆ … ┆ 0.0 ┆ 0.0 ┆ 3.0  ┆ 2.0  │
    #> │ …    ┆ …   ┆ …     ┆ …     ┆ … ┆ …   ┆ …   ┆ …    ┆ …    │
    #> │ 30.4 ┆ 4.0 ┆ 95.1  ┆ 113.0 ┆ … ┆ 1.0 ┆ 1.0 ┆ 5.0  ┆ 2.0  │
    #> │ 15.8 ┆ 8.0 ┆ 351.0 ┆ 264.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 4.0  │
    #> │ 19.7 ┆ 6.0 ┆ 145.0 ┆ 175.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 6.0  │
    #> │ 15.0 ┆ 8.0 ┆ 301.0 ┆ 335.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 8.0  │
    #> │ 21.4 ┆ 4.0 ┆ 121.0 ┆ 109.0 ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 2.0  │
    #> └──────┴─────┴───────┴───────┴───┴─────┴─────┴──────┴──────┘

``` r
# custom schema
pl$DataFrame(iris, schema = list(Sepal.Length = pl$Float32, Species = pl$String))
```

    #> shape: (150, 5)
    #> ┌──────────────┬─────────────┬──────────────┬─────────────┬───────────┐
    #> │ Sepal.Length ┆ Sepal.Width ┆ Petal.Length ┆ Petal.Width ┆ Species   │
    #> │ ---          ┆ ---         ┆ ---          ┆ ---         ┆ ---       │
    #> │ f32          ┆ f64         ┆ f64          ┆ f64         ┆ str       │
    #> ╞══════════════╪═════════════╪══════════════╪═════════════╪═══════════╡
    #> │ 5.1          ┆ 3.5         ┆ 1.4          ┆ 0.2         ┆ setosa    │
    #> │ 4.9          ┆ 3.0         ┆ 1.4          ┆ 0.2         ┆ setosa    │
    #> │ 4.7          ┆ 3.2         ┆ 1.3          ┆ 0.2         ┆ setosa    │
    #> │ 4.6          ┆ 3.1         ┆ 1.5          ┆ 0.2         ┆ setosa    │
    #> │ 5.0          ┆ 3.6         ┆ 1.4          ┆ 0.2         ┆ setosa    │
    #> │ …            ┆ …           ┆ …            ┆ …           ┆ …         │
    #> │ 6.7          ┆ 3.0         ┆ 5.2          ┆ 2.3         ┆ virginica │
    #> │ 6.3          ┆ 2.5         ┆ 5.0          ┆ 1.9         ┆ virginica │
    #> │ 6.5          ┆ 3.0         ┆ 5.2          ┆ 2.0         ┆ virginica │
    #> │ 6.2          ┆ 3.4         ┆ 5.4          ┆ 2.3         ┆ virginica │
    #> │ 5.9          ┆ 3.0         ┆ 5.1          ┆ 1.8         ┆ virginica │
    #> └──────────────┴─────────────┴──────────────┴─────────────┴───────────┘
