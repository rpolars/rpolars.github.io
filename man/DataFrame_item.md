

# Return the element at the given row/column.

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/dataframe__frame.R#L2353)

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
<code id="DataFrame_item_:_row">row</code>
</td>
<td>
Optional row index (0-indexed).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_item_:_column">column</code>
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
