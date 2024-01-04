
# Clone a Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/#L)

## Description

Rarely useful as Series are nearly 100% immutable Any modification of a
Series should lead to a clone anyways.

## Usage

<pre><code class='language-R'>Series_clone
</code></pre>

## Value

Series

## Examples

``` r
library(polars)

s1 = pl$Series(1:3)
s2 = s1$clone()
s3 = s1
pl$mem_address(s1) != pl$mem_address(s2)
```

    #> [1] TRUE

``` r
pl$mem_address(s1) == pl$mem_address(s3)
```

    #> [1] TRUE
