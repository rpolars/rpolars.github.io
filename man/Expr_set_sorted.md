
# Flag an Expr as "sorted"

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/expr__expr.R#L3312)

## Description

This enables downstream code to use fast paths for sorted arrays.
WARNING: this doesn’t check whether the data is actually sorted, you
have to ensure of that yourself.

## Usage

<pre><code class='language-R'>Expr_set_sorted(descending = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_set_sorted_:_descending">descending</code>
</td>
<td>
Sort the columns in descending order.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

# correct use flag something correctly as ascendingly sorted
s = pl$select(pl$lit(1:4)$set_sorted()$alias("a"))$get_column("a")
s$flags
```

    #> $SORTED_ASC
    #> [1] TRUE
    #> 
    #> $SORTED_DESC
    #> [1] FALSE

``` r
# incorrect use, flag something as not sorted ascendingly
s2 = pl$select(pl$lit(c(1, 3, 2, 4))$set_sorted()$alias("a"))$get_column("a")
s2$sort()
```

    #> polars Series: shape: (4,)
    #> Series: 'a' [f64]
    #> [
    #>  1.0
    #>  3.0
    #>  2.0
    #>  4.0
    #> ]

``` r
s2$flags # returns TRUE while it's not actually sorted
```

    #> $SORTED_ASC
    #> [1] TRUE
    #> 
    #> $SORTED_DESC
    #> [1] FALSE
