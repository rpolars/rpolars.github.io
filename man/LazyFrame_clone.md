

# Clone a LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L1677)

## Description

This makes a very cheap deep copy/clone of an existing
<code>LazyFrame</code>. Rarely useful as <code>LazyFrame</code>s are
nearly 100% immutable. Any modification of a <code>LazyFrame</code>
should lead to a clone anyways, but this can be useful when dealing with
attributes (see examples).

## Usage

<pre><code class='language-R'>LazyFrame_clone()
</code></pre>

## Value

A LazyFrame

## Examples

``` r
library(polars)

df1 = pl$LazyFrame(iris)

# Make a function to take a LazyFrame, add an attribute, and return a LazyFrame
give_attr = function(data) {
  attr(data, "created_on") = "2024-01-29"
  data
}
df2 = give_attr(df1)

# Problem: the original LazyFrame also gets the attribute while it shouldn't!
attributes(df1)
```

    #> $class
    #> [1] "RPolarsLazyFrame"
    #> 
    #> $created_on
    #> [1] "2024-01-29"

``` r
# Use $clone() inside the function to avoid that
give_attr = function(data) {
  data = data$clone()
  attr(data, "created_on") = "2024-01-29"
  data
}
df1 = pl$LazyFrame(iris)
df2 = give_attr(df1)

# now, the original LazyFrame doesn't get this attribute
attributes(df1)
```

    #> $class
    #> [1] "RPolarsLazyFrame"
