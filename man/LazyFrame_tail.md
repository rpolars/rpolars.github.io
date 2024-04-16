

# Get the last <code>n</code> rows.

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L1122)

## Description

Get the last <code>n</code> rows.

## Usage

<pre><code class='language-R'>LazyFrame_tail(n = 5L)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_tail_:_n">n</code>
</td>
<td>
Number of rows to return.
</td>
</tr>
</table>

## Value

A new <code>LazyFrame</code> object with applied filter.

## See Also

<code>\<LazyFrame\>$head()</code>

## Examples

``` r
library(polars)

lf = pl$LazyFrame(a = 1:6, b = 7:12)

lf$tail()$collect()
```

    #> shape: (5, 2)
    #> ┌─────┬─────┐
    #> │ a   ┆ b   │
    #> │ --- ┆ --- │
    #> │ i32 ┆ i32 │
    #> ╞═════╪═════╡
    #> │ 2   ┆ 8   │
    #> │ 3   ┆ 9   │
    #> │ 4   ┆ 10  │
    #> │ 5   ┆ 11  │
    #> │ 6   ┆ 12  │
    #> └─────┴─────┘

``` r
lf$tail(2)$collect()
```

    #> shape: (2, 2)
    #> ┌─────┬─────┐
    #> │ a   ┆ b   │
    #> │ --- ┆ --- │
    #> │ i32 ┆ i32 │
    #> ╞═════╪═════╡
    #> │ 5   ┆ 11  │
    #> │ 6   ┆ 12  │
    #> └─────┴─────┘
