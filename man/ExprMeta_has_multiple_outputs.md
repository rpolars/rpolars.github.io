
# Has multiple outputs

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/expr__meta.R#L136)

## Description

Whether this expression expands into multiple expressions.

## Usage

<pre><code class='language-R'>ExprMeta_has_multiple_outputs()
</code></pre>

## Value

Bool

## Examples

``` r
library(polars)

pl$all()$meta$has_multiple_outputs()
```

    #> [1] TRUE

``` r
pl$col("some_colname")$meta$has_multiple_outputs()
```

    #> [1] FALSE
