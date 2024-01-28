

# Clone a LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/lazyframe__lazy.R#L1658)

## Description

This makes a very cheap deep copy/clone of an existing
<code>LazyFrame</code>.

## Usage

<pre><code class='language-R'>LazyFrame_clone()
</code></pre>

## Value

A LazyFrame

## Examples

``` r
library(polars)

df1 = pl$LazyFrame(iris)
df2 = df1$clone()
df3 = df1

# the clone and the original don't have the same address...
pl$mem_address(df1) != pl$mem_address(df2)
```

    #> [1] TRUE

``` r
# ... but simply assigning df1 to df3 change the address anyway
pl$mem_address(df1) == pl$mem_address(df3)
```

    #> [1] TRUE
