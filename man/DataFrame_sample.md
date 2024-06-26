

# Take a sample of rows from a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L1852)

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
<code id="n">n</code>
</td>
<td>
Number of rows to return. Cannot be used with <code>fraction</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="fraction">fraction</code>
</td>
<td>
Fraction of rows to return (between 0 and 1). Cannot be used with
<code>n</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="with_replacement">with_replacement</code>
</td>
<td>
Allow values to be sampled more than once.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="shuffle">shuffle</code>
</td>
<td>
If <code>TRUE</code>, the order of the sampled rows will be shuffled. If
<code>FALSE</code> (default), the order of the returned rows will be
neither stable nor fully random.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="seed">seed</code>
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
    #> │ 5.8          ┆ 2.8         ┆ 5.1          ┆ 2.4         ┆ virginica  │
    #> │ 5.6          ┆ 2.9         ┆ 3.6          ┆ 1.3         ┆ versicolor │
    #> │ 5.0          ┆ 3.4         ┆ 1.5          ┆ 0.2         ┆ setosa     │
    #> │ 5.6          ┆ 2.8         ┆ 4.9          ┆ 2.0         ┆ virginica  │
    #> │ 4.9          ┆ 3.1         ┆ 1.5          ┆ 0.2         ┆ setosa     │
    #> │ …            ┆ …           ┆ …            ┆ …           ┆ …          │
    #> │ 5.4          ┆ 3.0         ┆ 4.5          ┆ 1.5         ┆ versicolor │
    #> │ 6.7          ┆ 3.3         ┆ 5.7          ┆ 2.1         ┆ virginica  │
    #> │ 4.9          ┆ 3.1         ┆ 1.5          ┆ 0.1         ┆ setosa     │
    #> │ 5.4          ┆ 3.9         ┆ 1.3          ┆ 0.4         ┆ setosa     │
    #> │ 5.6          ┆ 2.5         ┆ 3.9          ┆ 1.1         ┆ versicolor │
    #> └──────────────┴─────────────┴──────────────┴─────────────┴────────────┘

``` r
df$sample(frac = 0.1)
```

    #> shape: (15, 5)
    #> ┌──────────────┬─────────────┬──────────────┬─────────────┬───────────┐
    #> │ Sepal.Length ┆ Sepal.Width ┆ Petal.Length ┆ Petal.Width ┆ Species   │
    #> │ ---          ┆ ---         ┆ ---          ┆ ---         ┆ ---       │
    #> │ f64          ┆ f64         ┆ f64          ┆ f64         ┆ cat       │
    #> ╞══════════════╪═════════════╪══════════════╪═════════════╪═══════════╡
    #> │ 7.7          ┆ 2.6         ┆ 6.9          ┆ 2.3         ┆ virginica │
    #> │ 5.2          ┆ 3.4         ┆ 1.4          ┆ 0.2         ┆ setosa    │
    #> │ 5.5          ┆ 3.5         ┆ 1.3          ┆ 0.2         ┆ setosa    │
    #> │ 5.0          ┆ 3.4         ┆ 1.5          ┆ 0.2         ┆ setosa    │
    #> │ 6.4          ┆ 2.8         ┆ 5.6          ┆ 2.2         ┆ virginica │
    #> │ …            ┆ …           ┆ …            ┆ …           ┆ …         │
    #> │ 5.0          ┆ 3.5         ┆ 1.3          ┆ 0.3         ┆ setosa    │
    #> │ 6.5          ┆ 3.0         ┆ 5.8          ┆ 2.2         ┆ virginica │
    #> │ 6.3          ┆ 3.3         ┆ 6.0          ┆ 2.5         ┆ virginica │
    #> │ 5.8          ┆ 2.7         ┆ 5.1          ┆ 1.9         ┆ virginica │
    #> │ 5.7          ┆ 4.4         ┆ 1.5          ┆ 0.4         ┆ setosa    │
    #> └──────────────┴─────────────┴──────────────┴─────────────┴───────────┘
