

# Limit a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/dataframe__frame.R#L767)

## Description

Take some maximum number of rows.

## Usage

<pre><code class='language-R'>DataFrame_limit(n)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_limit_:_n">n</code>
</td>
<td>
Positive number not larger than 2^32.
</td>
</tr>
</table>

## Details

Any number will converted to u32. Negative raises error.

## Value

DataFrame

## Examples

``` r
library(polars)

pl$DataFrame(iris)$limit(6)
```

    #> shape: (6, 5)
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
    #> │ 5.4          ┆ 3.9         ┆ 1.7          ┆ 0.4         ┆ setosa  │
    #> └──────────────┴─────────────┴──────────────┴─────────────┴─────────┘
