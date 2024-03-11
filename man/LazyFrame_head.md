

# Get the first <code>n</code> rows.

[**Source code**](https://github.com/pola-rs/r-polars/tree/c47431ca69622f79ed7a3f1d7bfee6075ffabfee/R/lazyframe__lazy.R#L865)

## Description

A shortcut for <code>$slice(0, n)</code>. Consider using the
<code>$fetch()</code> method if you want to test your query. The
<code>$fetch()</code> operation will load the first <code>n</code> rows
at the scan level, whereas
<code style="white-space: pre;">$head()</code> is applied at the end.

## Usage

<pre><code class='language-R'>LazyFrame_head(n = 5L)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_head_:_n">n</code>
</td>
<td>
Number of rows to return.
</td>
</tr>
</table>

## Details

<code style="white-space: pre;">$limit()</code> is an alias for
<code style="white-space: pre;">$head()</code>.

## Value

A new <code>LazyFrame</code> object with applied filter.

## Examples

``` r
library(polars)

lf = pl$LazyFrame(a = 1:6, b = 7:12)

lf$head()$collect()
```

    #> shape: (5, 2)
    #> ┌─────┬─────┐
    #> │ a   ┆ b   │
    #> │ --- ┆ --- │
    #> │ i32 ┆ i32 │
    #> ╞═════╪═════╡
    #> │ 1   ┆ 7   │
    #> │ 2   ┆ 8   │
    #> │ 3   ┆ 9   │
    #> │ 4   ┆ 10  │
    #> │ 5   ┆ 11  │
    #> └─────┴─────┘

``` r
lf$head(2)$collect()
```

    #> shape: (2, 2)
    #> ┌─────┬─────┐
    #> │ a   ┆ b   │
    #> │ --- ┆ --- │
    #> │ i32 ┆ i32 │
    #> ╞═════╪═════╡
    #> │ 1   ┆ 7   │
    #> │ 2   ┆ 8   │
    #> └─────┴─────┘
