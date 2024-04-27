

# Gather every nth element

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__expr.R#L2015)

## Description

Gather every nth value in the Series and return as a new Series.

## Usage

<pre><code class='language-R'>Expr_gather_every(n, offset = 0)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="n">n</code>
</td>
<td>
Positive integer.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="offset">offset</code>
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
