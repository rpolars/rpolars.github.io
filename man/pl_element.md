

# an element in ‘eval’-expr

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/functions__lazy.R#L82)

## Description

Alias for an element in evaluated in an <code>eval</code> expression.

## Usage

<pre><code class='language-R'>pl_element()
</code></pre>

## Value

Expr

## Examples

``` r
library(polars)

pl$lit(1:5)$cumulative_eval(pl$element()$first() - pl$element()$last()**2)$to_r()
```

    #> [1]   0  -3  -8 -15 -24
