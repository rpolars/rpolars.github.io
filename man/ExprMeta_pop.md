

# Pop

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__meta.R#L68)

## Description

Pop the latest expression and return the input(s) of the popped
expression.

## Usage

<pre><code class='language-R'>ExprMeta_pop()
</code></pre>

## Value

A list of expressions which in most cases will have a unit length. This
is not the case when an expression has multiple inputs, for instance in
a <code>$fold()</code> expression.

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
