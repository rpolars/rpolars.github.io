
# Approximate count of unique values.

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L424)

## Description

This is done using the HyperLogLog++ algorithm for cardinality
estimation.

## Usage

<pre><code class='language-R'>pl_approx_n_unique(column)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_approx_n_unique_:_column">column</code>
</td>
<td>

if dtype is:

<ul>
<li>

String: syntactic sugar for
<code>pl$col(column)$approx_n_unique()</code>, returns Expr

</li>
<li>

Expr: syntactic sugar for <code>column$approx_n_unique()</code>, returns
Expr

</li>
</ul>
</td>
</tr>
</table>

## Details

The approx_n_unique is likely only warranted for large columns. See
example. It appears approx_n_unique scales better than n_unique, such
that the relative performance difference increases with column size.

## Value

Expr

## Examples

``` r
library(polars)

# column as Series
pl$approx_n_unique(pl$lit(1:4)) == 4
```

    #> polars Expr: [(Series.approx_n_unique()) == (4.0)]

``` r
# column as String
expr = pl$approx_n_unique("bob")
print(expr)
```

    #> polars Expr: col("bob").approx_n_unique()

``` r
pl$DataFrame(bob = 1:80)$select(expr)
```

    #> shape: (1, 1)
    #> ┌─────┐
    #> │ bob │
    #> │ --- │
    #> │ u32 │
    #> ╞═════╡
    #> │ 79  │
    #> └─────┘

``` r
# colum as Expr
pl$DataFrame(bob = 1:4)$select(pl$approx_n_unique(pl$col("bob")))
```

    #> shape: (1, 1)
    #> ┌─────┐
    #> │ bob │
    #> │ --- │
    #> │ u32 │
    #> ╞═════╡
    #> │ 4   │
    #> └─────┘

``` r
# comparison with n_unique for 2 million integers. (try change example to 20 million ints)
lit_series = pl$lit(c(1:1E6, 1E6:1, 1:1E6))
system.time(pl$approx_n_unique(lit_series)$to_series()$print())
```

    #> shape: (1,)
    #> Series: '' [u32]
    #> [
    #>  1014256
    #> ]

    #>    user  system elapsed 
    #>   0.029   0.000   0.029

``` r
system.time(pl$n_unique(lit_series)$to_series()$print())
```

    #> shape: (1,)
    #> Series: '' [u32]
    #> [
    #>  1000000
    #> ]

    #>    user  system elapsed 
    #>   0.114   0.004   0.065
