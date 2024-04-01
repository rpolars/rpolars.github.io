

# Get the first <code>n</code> rows.

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L889)

## Description

Get the first <code>n</code> rows.

## Usage

<pre><code class='language-R'>DataFrame_head(n = 5L)

DataFrame_limit(n = 5L)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_head_:_n">n</code>
</td>
<td>
Number of rows to return. If a negative value is passed, return all rows
except the last <code>abs(n)</code>.
</td>
</tr>
</table>

## Details

<code style="white-space: pre;">$limit()</code> is an alias for
<code style="white-space: pre;">$head()</code>.

## Value

A DataFrame

## Examples

``` r
library(polars)

df = pl$DataFrame(foo = 1:5, bar = 6:10, ham = letters[1:5])

df$head(3)
```

    #> shape: (3, 3)
    #> ┌─────┬─────┬─────┐
    #> │ foo ┆ bar ┆ ham │
    #> │ --- ┆ --- ┆ --- │
    #> │ i32 ┆ i32 ┆ str │
    #> ╞═════╪═════╪═════╡
    #> │ 1   ┆ 6   ┆ a   │
    #> │ 2   ┆ 7   ┆ b   │
    #> │ 3   ┆ 8   ┆ c   │
    #> └─────┴─────┴─────┘

``` r
# Pass a negative value to get all rows except the last `abs(n)`.
df$head(-3)
```

    #> shape: (2, 3)
    #> ┌─────┬─────┬─────┐
    #> │ foo ┆ bar ┆ ham │
    #> │ --- ┆ --- ┆ --- │
    #> │ i32 ┆ i32 ┆ str │
    #> ╞═════╪═════╪═════╡
    #> │ 1   ┆ 6   ┆ a   │
    #> │ 2   ┆ 7   ┆ b   │
    #> └─────┴─────┴─────┘
