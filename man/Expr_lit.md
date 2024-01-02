
# Create a literal value

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/expr__expr.R#L934)

## Description

Create a literal value

## Usage

<pre><code class='language-R'>Expr_lit(x)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_lit_:_x">x</code>
</td>
<td>
A vector of any length
</td>
</tr>
</table>

## Details

<code>pl$lit(NULL)</code> translates into a polars <code>null</code>.

## Value

Expr

## Examples

``` r
library(polars)

# scalars to literal, explicit `pl$lit(42)` implicit `+ 2`
pl$col("some_column") / pl$lit(42) + 2
```

    #> polars Expr: [([(col("some_column")) // (42.0)]) + (2.0)]

``` r
# vector to literal explicitly via Series and back again
# R vector to expression and back again
pl$select(pl$lit(pl$Series(1:4)))$to_list()[[1L]]
```

    #> [1] 1 2 3 4

``` r
# r vector to literal and back r vector
pl$lit(1:4)$to_r()
```

    #> [1] 1 2 3 4

``` r
# r vector to literal to dataframe
pl$select(pl$lit(1:4))
```

    #> shape: (4, 1)
    #> ┌─────┐
    #> │     │
    #> │ --- │
    #> │ i32 │
    #> ╞═════╡
    #> │ 1   │
    #> │ 2   │
    #> │ 3   │
    #> │ 4   │
    #> └─────┘

``` r
# r vector to literal to Series
pl$lit(1:4)$to_series()
```

    #> polars Series: shape: (4,)
    #> Series: '' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #>  4
    #> ]

``` r
# vectors to literal implicitly
(pl$lit(2) + 1:4) / 4:1
```

    #> polars Expr: [([(2.0) + (Series)]) // (Series)]
