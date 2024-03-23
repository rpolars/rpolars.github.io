

# Gather every nth element

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L2022)

## Description

Gather every nth value in the Series and return as a new Series.

## Usage

<pre><code class='language-R'>Expr_gather_every(n, offset = 0)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_gather_every_:_n">n</code>
</td>
<td>
Positive integer.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_gather_every_:_offset">offset</code>
</td>
<td>
Starting index.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = 0:24)$select(pl$col("a")$gather_every(6))
```

    #> shape: (5, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ i32 │
    #> ╞═════╡
    #> │ 0   │
    #> │ 6   │
    #> │ 12  │
    #> │ 18  │
    #> │ 24  │
    #> └─────┘
