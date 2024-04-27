

# Negate a boolean expression

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/after-wrappers.R#L20)

## Description

Method equivalent of negation operator <code>!expr</code>.

## Usage

<pre><code class='language-R'>Expr_not()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

# two syntaxes same result
pl$lit(TRUE)$not()
```

    #> polars Expr: true.not()

``` r
!pl$lit(TRUE)
```

    #> polars Expr: true.not()
