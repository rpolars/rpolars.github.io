

# Repeat a Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L3093)

## Description

This expression takes input and repeats it n times and append chunk.

## Usage

<pre><code class='language-R'>Expr_rep(n, rechunk = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_rep_:_n">n</code>
</td>
<td>
The number of times to repeat, must be non-negative and finite.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_rep_:_rechunk">rechunk</code>
</td>
<td>
If <code>TRUE</code> (default), memory layout will be rewritten.
</td>
</tr>
</table>

## Details

If the input has length 1, this uses a special faster implementation
that doesn’t require rechunking (so <code>rechunk = TRUE</code> has no
effect).

## Value

Expr

## Examples

``` r
library(polars)

pl$select(pl$lit("alice")$rep(n = 3))
```

    #> shape: (3, 1)
    #> ┌─────────┐
    #> │ literal │
    #> │ ---     │
    #> │ str     │
    #> ╞═════════╡
    #> │ alice   │
    #> │ alice   │
    #> │ alice   │
    #> └─────────┘

``` r
pl$select(pl$lit(1:3)$rep(n = 2))
```

    #> shape: (6, 1)
    #> ┌─────┐
    #> │     │
    #> │ --- │
    #> │ i32 │
    #> ╞═════╡
    #> │ 1   │
    #> │ 2   │
    #> │ 3   │
    #> │ 1   │
    #> │ 2   │
    #> │ 3   │
    #> └─────┘
