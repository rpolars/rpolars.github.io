
# an element in ‘eval’-expr

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/functions__lazy.R#L81)

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
