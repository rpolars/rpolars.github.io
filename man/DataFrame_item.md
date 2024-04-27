

# Return the element at the given row/column.

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/dataframe__frame.R#L2353)

## Description

If row and column location are not specified, the DataFrame must have
dimensions (1, 1).

## Usage

<pre><code class='language-R'>DataFrame_item(row = NULL, column = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="row">row</code>
</td>
<td>
Optional row index (0-indexed).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="column">column</code>
</td>
<td>
Optional column index (0-indexed) or name.
</td>
</tr>
</table>

## Value

A value of length 1

## Examples

``` r
library(polars)

df = pl$DataFrame(a = c(1, 2, 3), b = c(4, 5, 6))

df$select((pl$col("a") * pl$col("b"))$sum())$item()
```

    #> [1] 32

``` r
df$item(1, 1)
```

    #> [1] 5

``` r
df$item(2, "b")
```

    #> [1] 6
