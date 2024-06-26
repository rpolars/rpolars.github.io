

# Extend Series with a constant

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L3021)

## Description

Extend the Series with given number of values.

## Usage

<pre><code class='language-R'>Expr_extend_constant(value, n)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="value">value</code>
</td>
<td>
The value to extend the Series with. This value may be <code>NULL</code>
to fill with nulls.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="n">n</code>
</td>
<td>
The number of values to extend.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

pl$select(pl$lit(1:4)$extend_constant(10.1, 2))
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
    #> │ 4   │
    #> │ 10  │
    #> │ 10  │
    #> └─────┘

``` r
pl$select(pl$lit(1:4)$extend_constant(NULL, 2))
```

    #> shape: (6, 1)
    #> ┌──────┐
    #> │      │
    #> │ ---  │
    #> │ i32  │
    #> ╞══════╡
    #> │ 1    │
    #> │ 2    │
    #> │ 3    │
    #> │ 4    │
    #> │ null │
    #> │ null │
    #> └──────┘
