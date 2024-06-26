

# Get the last <code>n</code> rows.

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L916)

## Description

Get the last <code>n</code> rows.

## Usage

<pre><code class='language-R'>DataFrame_tail(n = 5L)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="n">n</code>
</td>
<td>
Number of rows to return. If a negative value is passed, return all rows
except the first <code>abs(n)</code>.
</td>
</tr>
</table>

## Value

A DataFrame

## Examples

``` r
library(polars)

df = pl$DataFrame(foo = 1:5, bar = 6:10, ham = letters[1:5])

df$tail(3)
```

    #> shape: (3, 3)
    #> ┌─────┬─────┬─────┐
    #> │ foo ┆ bar ┆ ham │
    #> │ --- ┆ --- ┆ --- │
    #> │ i32 ┆ i32 ┆ str │
    #> ╞═════╪═════╪═════╡
    #> │ 3   ┆ 8   ┆ c   │
    #> │ 4   ┆ 9   ┆ d   │
    #> │ 5   ┆ 10  ┆ e   │
    #> └─────┴─────┴─────┘

``` r
# Pass a negative value to get all rows except the first `abs(n)`.
df$tail(-3)
```

    #> shape: (2, 3)
    #> ┌─────┬─────┬─────┐
    #> │ foo ┆ bar ┆ ham │
    #> │ --- ┆ --- ┆ --- │
    #> │ i32 ┆ i32 ┆ str │
    #> ╞═════╪═════╪═════╡
    #> │ 4   ┆ 9   ┆ d   │
    #> │ 5   ┆ 10  ┆ e   │
    #> └─────┴─────┴─────┘
