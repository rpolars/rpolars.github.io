

# Summary statistics for a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L1513)

## Description

This returns the total number of rows, the number of missing values, the
mean, standard deviation, min, max, median and the percentiles specified
in the argument <code>percentiles</code>.

## Usage

<pre><code class='language-R'>DataFrame_describe(percentiles = c(0.25, 0.75), interpolation = "nearest")
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_describe_:_percentiles">percentiles</code>
</td>
<td>
One or more percentiles to include in the summary statistics. All values
must be in the range <code style="white-space: pre;">\[0; 1\]</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_describe_:_interpolation">interpolation</code>
</td>
<td>
Interpolation method for computing quantiles. One of
<code>“nearest”</code>, <code>“higher”</code>, <code>“lower”</code>,
<code>“midpoint”</code>, or <code>“linear”</code>.
</td>
</tr>
</table>

## Value

DataFrame

## Examples

``` r
library(polars)

pl$DataFrame(iris)$describe()
```

    #> shape: (9, 6)
    #> ┌────────────┬──────────────┬─────────────┬──────────────┬─────────────┬─────────┐
    #> │ describe   ┆ Sepal.Length ┆ Sepal.Width ┆ Petal.Length ┆ Petal.Width ┆ Species │
    #> │ ---        ┆ ---          ┆ ---         ┆ ---          ┆ ---         ┆ ---     │
    #> │ str        ┆ f64          ┆ f64         ┆ f64          ┆ f64         ┆ f64     │
    #> ╞════════════╪══════════════╪═════════════╪══════════════╪═════════════╪═════════╡
    #> │ count      ┆ 150.0        ┆ 150.0       ┆ 150.0        ┆ 150.0       ┆ 150.0   │
    #> │ null_count ┆ 0.0          ┆ 0.0         ┆ 0.0          ┆ 0.0         ┆ 0.0     │
    #> │ mean       ┆ 5.843333     ┆ 3.057333    ┆ 3.758        ┆ 1.199333    ┆ null    │
    #> │ std        ┆ 0.828066     ┆ 0.435866    ┆ 1.765298     ┆ 0.762238    ┆ null    │
    #> │ min        ┆ 4.3          ┆ 2.0         ┆ 1.0          ┆ 0.1         ┆ null    │
    #> │ 25%        ┆ 5.1          ┆ 2.8         ┆ 1.6          ┆ 0.3         ┆ null    │
    #> │ 50%        ┆ 5.8          ┆ 3.0         ┆ 4.4          ┆ 1.3         ┆ null    │
    #> │ 75%        ┆ 6.4          ┆ 3.3         ┆ 5.1          ┆ 1.8         ┆ null    │
    #> │ max        ┆ 7.9          ┆ 4.4         ┆ 6.9          ┆ 2.5         ┆ null    │
    #> └────────────┴──────────────┴─────────────┴──────────────┴─────────────┴─────────┘

``` r
# string, date, boolean columns are also supported:
df = pl$DataFrame(
  int = 1:3,
  string = c(letters[1:2], NA),
  date = c(as.Date("2024-01-20"), as.Date("2024-01-21"), NA),
  cat = factor(c(letters[1:2], NA)),
  bool = c(TRUE, FALSE, NA)
)
df
```

    #> shape: (3, 5)
    #> ┌─────┬────────┬────────────┬──────┬───────┐
    #> │ int ┆ string ┆ date       ┆ cat  ┆ bool  │
    #> │ --- ┆ ---    ┆ ---        ┆ ---  ┆ ---   │
    #> │ i32 ┆ str    ┆ date       ┆ cat  ┆ bool  │
    #> ╞═════╪════════╪════════════╪══════╪═══════╡
    #> │ 1   ┆ a      ┆ 2024-01-20 ┆ a    ┆ true  │
    #> │ 2   ┆ b      ┆ 2024-01-21 ┆ b    ┆ false │
    #> │ 3   ┆ null   ┆ null       ┆ null ┆ null  │
    #> └─────┴────────┴────────────┴──────┴───────┘

``` r
df$describe()
```

    #> shape: (9, 6)
    #> ┌────────────┬─────┬────────┬────────────┬──────┬───────┐
    #> │ describe   ┆ int ┆ string ┆ date       ┆ cat  ┆ bool  │
    #> │ ---        ┆ --- ┆ ---    ┆ ---        ┆ ---  ┆ ---   │
    #> │ str        ┆ str ┆ str    ┆ str        ┆ str  ┆ str   │
    #> ╞════════════╪═════╪════════╪════════════╪══════╪═══════╡
    #> │ count      ┆ 3   ┆ 2      ┆ 2          ┆ 2    ┆ 2     │
    #> │ null_count ┆ 0   ┆ 1      ┆ 1          ┆ 1    ┆ 1     │
    #> │ mean       ┆ 2.0 ┆ null   ┆ null       ┆ null ┆ null  │
    #> │ std        ┆ 1.0 ┆ null   ┆ null       ┆ null ┆ null  │
    #> │ min        ┆ 1   ┆ a      ┆ 2024-01-20 ┆ null ┆ false │
    #> │ 25%        ┆ 2.0 ┆ null   ┆ null       ┆ null ┆ null  │
    #> │ 50%        ┆ 2.0 ┆ null   ┆ null       ┆ null ┆ null  │
    #> │ 75%        ┆ 3.0 ┆ null   ┆ null       ┆ null ┆ null  │
    #> │ max        ┆ 3   ┆ b      ┆ 2024-01-21 ┆ null ┆ true  │
    #> └────────────┴─────┴────────┴────────────┴──────┴───────┘
