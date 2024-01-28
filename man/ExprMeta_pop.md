

# Pop

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/expr__meta.R#L73)

## Description

Pop the latest expression and return the input(s) of the popped
expression.

## Usage

<pre><code class='language-R'>ExprMeta_pop()
</code></pre>

## Value

R list of Expr(s) usually one, only multiple if top Expr took more Expr
as input.

## Examples

``` r
library(polars)

e1 = pl$lit(40) + 2
e2 = pl$lit(42)$sum()

e1
```

    #> polars Expr: [(40.0) + (2.0)]

``` r
e1$meta$pop()
```

    #> [[1]]
    #> polars Expr: 2.0
    #> 
    #> [[2]]
    #> polars Expr: 40.0

``` r
e2
```

    #> polars Expr: 42.0.sum()

``` r
e2$meta$pop()
```

    #> [[1]]
    #> polars Expr: 42.0
