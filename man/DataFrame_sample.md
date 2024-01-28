

# Take a sample of rows from a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/dataframe__frame.R#L1727)

## Description

Take a sample of rows from a DataFrame

## Usage

<pre><code class='language-R'>DataFrame_sample(
  n = NULL,
  fraction = NULL,
  with_replacement = FALSE,
  shuffle = FALSE,
  seed = NULL
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_sample_:_n">n</code>
</td>
<td>
Number of rows to return. Cannot be used with <code>fraction</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_sample_:_fraction">fraction</code>
</td>
<td>
Fraction of rows to return (between 0 and 1). Cannot be used with
<code>n</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_sample_:_with_replacement">with_replacement</code>
</td>
<td>
Allow values to be sampled more than once.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_sample_:_shuffle">shuffle</code>
</td>
<td>
If <code>TRUE</code>, the order of the sampled rows will be shuffled. If
<code>FALSE</code> (default), the order of the returned rows will be
neither stable nor fully random.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_sample_:_seed">seed</code>
</td>
<td>
Seed for the random number generator. If set to <code>NULL</code>
(default), a random seed is generated for each sample operation.
</td>
</tr>
</table>

## Value

DataFrame

## Examples

``` r
library(polars)

df = pl$DataFrame(iris)
df$sample(n = 20)
```

    #> shape: (20, 5)
    #> ┌──────────────┬─────────────┬──────────────┬─────────────┬────────────┐
    #> │ Sepal.Length ┆ Sepal.Width ┆ Petal.Length ┆ Petal.Width ┆ Species    │
    #> │ ---          ┆ ---         ┆ ---          ┆ ---         ┆ ---        │
    #> │ f64          ┆ f64         ┆ f64          ┆ f64         ┆ cat        │
    #> ╞══════════════╪═════════════╪══════════════╪═════════════╪════════════╡
    #> │ 5.5          ┆ 2.5         ┆ 4.0          ┆ 1.3         ┆ versicolor │
    #> │ 6.3          ┆ 2.7         ┆ 4.9          ┆ 1.8         ┆ virginica  │
    #> │ 5.7          ┆ 2.5         ┆ 5.0          ┆ 2.0         ┆ virginica  │
    #> │ 5.1          ┆ 3.3         ┆ 1.7          ┆ 0.5         ┆ setosa     │
    #> │ …            ┆ …           ┆ …            ┆ …           ┆ …          │
    #> │ 6.5          ┆ 3.0         ┆ 5.8          ┆ 2.2         ┆ virginica  │
    #> │ 4.8          ┆ 3.4         ┆ 1.6          ┆ 0.2         ┆ setosa     │
    #> │ 7.3          ┆ 2.9         ┆ 6.3          ┆ 1.8         ┆ virginica  │
    #> │ 4.4          ┆ 3.0         ┆ 1.3          ┆ 0.2         ┆ setosa     │
    #> └──────────────┴─────────────┴──────────────┴─────────────┴────────────┘

``` r
df$sample(frac = 0.1)
```

    #> shape: (15, 5)
    #> ┌──────────────┬─────────────┬──────────────┬─────────────┬────────────┐
    #> │ Sepal.Length ┆ Sepal.Width ┆ Petal.Length ┆ Petal.Width ┆ Species    │
    #> │ ---          ┆ ---         ┆ ---          ┆ ---         ┆ ---        │
    #> │ f64          ┆ f64         ┆ f64          ┆ f64         ┆ cat        │
    #> ╞══════════════╪═════════════╪══════════════╪═════════════╪════════════╡
    #> │ 5.5          ┆ 2.3         ┆ 4.0          ┆ 1.3         ┆ versicolor │
    #> │ 6.5          ┆ 3.2         ┆ 5.1          ┆ 2.0         ┆ virginica  │
    #> │ 6.4          ┆ 2.7         ┆ 5.3          ┆ 1.9         ┆ virginica  │
    #> │ 5.2          ┆ 3.4         ┆ 1.4          ┆ 0.2         ┆ setosa     │
    #> │ …            ┆ …           ┆ …            ┆ …           ┆ …          │
    #> │ 6.2          ┆ 2.8         ┆ 4.8          ┆ 1.8         ┆ virginica  │
    #> │ 6.7          ┆ 3.3         ┆ 5.7          ┆ 2.5         ┆ virginica  │
    #> │ 6.4          ┆ 3.1         ┆ 5.5          ┆ 1.8         ┆ virginica  │
    #> │ 6.1          ┆ 2.6         ┆ 5.6          ┆ 1.4         ┆ virginica  │
    #> └──────────────┴─────────────┴──────────────┴─────────────┴────────────┘
