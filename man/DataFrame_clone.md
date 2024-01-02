
# Clone a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/dataframe__frame.R#L527)

## Description

This is rarely useful as a DataFrame is nearly 100% immutable. Any
modification of a DataFrame would lead to a clone anyway.

## Usage

<pre><code class='language-R'>DataFrame_clone()
</code></pre>

## Value

A DataFrame

## Examples

``` r
library(polars)

df1 = pl$DataFrame(iris)
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
