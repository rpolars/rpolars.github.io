

# Create an empty or n-row null-filled copy of the DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/dataframe__frame.R#L2418)

## Description

Returns a n-row null-filled DataFrame with an identical schema.
<code>n</code> can be greater than the current number of rows in the
DataFrame.

## Usage

<pre><code class='language-R'>DataFrame_clear(n = 0)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="n">n</code>
</td>
<td>
Number of (null-filled) rows to return in the cleared frame.
</td>
</tr>
</table>

## Value

A n-row null-filled DataFrame with an identical schema

## Examples

``` r
library(polars)

df = pl$DataFrame(
  a = c(NA, 2, 3, 4),
  b = c(0.5, NA, 2.5, 13),
  c = c(TRUE, TRUE, FALSE, NA)
)

df$clear()
```

    #> shape: (0, 3)
    #> ┌─────┬─────┬──────┐
    #> │ a   ┆ b   ┆ c    │
    #> │ --- ┆ --- ┆ ---  │
    #> │ f64 ┆ f64 ┆ bool │
    #> ╞═════╪═════╪══════╡
    #> └─────┴─────┴──────┘

``` r
df$clear(n = 5)
```

    #> shape: (5, 3)
    #> ┌──────┬──────┬──────┐
    #> │ a    ┆ b    ┆ c    │
    #> │ ---  ┆ ---  ┆ ---  │
    #> │ f64  ┆ f64  ┆ bool │
    #> ╞══════╪══════╪══════╡
    #> │ null ┆ null ┆ null │
    #> │ null ┆ null ┆ null │
    #> │ null ┆ null ┆ null │
    #> │ null ┆ null ┆ null │
    #> │ null ┆ null ┆ null │
    #> └──────┴──────┴──────┘
