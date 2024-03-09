

# Clone a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/mkdocs-matrial-search-preview/R/dataframe__frame.R#L595)

## Description

This makes a very cheap deep copy/clone of an existing
<code>DataFrame</code>. Rarely useful as <code>DataFrame</code>s are
nearly 100% immutable. Any modification of a <code>DataFrame</code>
should lead to a clone anyways, but this can be useful when dealing with
attributes (see examples).

## Usage

<pre><code class='language-R'>DataFrame_clone()
</code></pre>

## Value

A DataFrame

## Examples

``` r
library(polars)

df1 = pl$DataFrame(iris)

# Make a function to take a DataFrame, add an attribute, and return a DataFrame
give_attr = function(data) {
  attr(data, "created_on") = "2024-01-29"
  data
}
df2 = give_attr(df1)

# Problem: the original DataFrame also gets the attribute while it shouldn't!
attributes(df1)
```

    #> $class
    #> [1] "RPolarsDataFrame"
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
df1 = pl$DataFrame(iris)
df2 = give_attr(df1)

# now, the original DataFrame doesn't get this attribute
attributes(df1)
```

    #> $class
    #> [1] "RPolarsDataFrame"
