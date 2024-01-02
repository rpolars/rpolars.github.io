
# Any expr method on a Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/series__series.R#L935)

## Description

Call an expression on a Series See the individual Expr method pages for
full details

## Usage

<pre><code class='language-R'>Series_expr()
</code></pre>

## Details

This is a shorthand of writing something like
<code>pl$DataFrame(s)$select(pl$col(“sname”)$expr)$to_series(0)</code>

This subnamespace is experimental. Submit an issue if anything
unexpected happened.

## Value

Expr

## Examples

``` r
library(polars)

s = pl$Series(list(1:3, 1:2, NULL))
s$expr$first()
```

    #> polars Series: shape: (1,)
    #> Series: '' [list[i32]]
    #> [
    #>  [1, 2, 3]
    #> ]

``` r
s$expr$alias("alice")
```

    #> polars Series: shape: (3,)
    #> Series: 'alice' [list[i32]]
    #> [
    #>  [1, 2, 3]
    #>  [1, 2]
    #>  []
    #> ]
