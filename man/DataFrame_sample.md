

# Take a sample of rows from a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L1732)

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
    #> │ 7.7          ┆ 3.0         ┆ 6.1          ┆ 2.3         ┆ virginica  │
    #> │ 4.9          ┆ 3.0         ┆ 1.4          ┆ 0.2         ┆ setosa     │
    #> │ 6.2          ┆ 2.9         ┆ 4.3          ┆ 1.3         ┆ versicolor │
    #> │ 5.2          ┆ 4.1         ┆ 1.5          ┆ 0.1         ┆ setosa     │
    #> │ 6.4          ┆ 2.9         ┆ 4.3          ┆ 1.3         ┆ versicolor │
    #> │ …            ┆ …           ┆ …            ┆ …           ┆ …          │
    #> │ 6.7          ┆ 3.1         ┆ 4.7          ┆ 1.5         ┆ versicolor │
    #> │ 6.0          ┆ 2.2         ┆ 4.0          ┆ 1.0         ┆ versicolor │
    #> │ 6.2          ┆ 2.8         ┆ 4.8          ┆ 1.8         ┆ virginica  │
    #> │ 7.6          ┆ 3.0         ┆ 6.6          ┆ 2.1         ┆ virginica  │
    #> │ 6.8          ┆ 3.2         ┆ 5.9          ┆ 2.3         ┆ virginica  │
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
    #> │ 5.1          ┆ 3.8         ┆ 1.6          ┆ 0.2         ┆ setosa     │
    #> │ 6.2          ┆ 2.9         ┆ 4.3          ┆ 1.3         ┆ versicolor │
    #> │ 6.0          ┆ 2.9         ┆ 4.5          ┆ 1.5         ┆ versicolor │
    #> │ 6.8          ┆ 3.2         ┆ 5.9          ┆ 2.3         ┆ virginica  │
    #> │ 6.7          ┆ 3.1         ┆ 5.6          ┆ 2.4         ┆ virginica  │
    #> │ …            ┆ …           ┆ …            ┆ …           ┆ …          │
    #> │ 4.4          ┆ 3.0         ┆ 1.3          ┆ 0.2         ┆ setosa     │
    #> │ 5.0          ┆ 3.5         ┆ 1.3          ┆ 0.3         ┆ setosa     │
    #> │ 5.6          ┆ 2.7         ┆ 4.2          ┆ 1.3         ┆ versicolor │
    #> │ 5.7          ┆ 2.8         ┆ 4.1          ┆ 1.3         ┆ versicolor │
    #> │ 7.9          ┆ 3.8         ┆ 6.4          ┆ 2.0         ┆ virginica  │
    #> └──────────────┴─────────────┴──────────────┴─────────────┴────────────┘
