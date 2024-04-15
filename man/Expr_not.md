

# Negate a boolean expression

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/after-wrappers.R#L20)

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
