

# Clone a Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/after-wrappers.R#L20)

## Description

This makes a very cheap deep copy/clone of an existing
<code>Series</code>. Rarely useful as <code>Series</code> are nearly
100% immutable. Any modification of a <code>Series</code> should lead to
a clone anyways, but this can be useful when dealing with attributes
(see examples).

## Usage

<pre><code class='language-R'>Series_clone()
</code></pre>

## Value

Series

## Examples

``` r
library(polars)

df1 = as_polars_series(1:10)

# Make a function to take a Series, add an attribute, and return a Series
give_attr = function(data) {
  attr(data, "created_on") = "2024-01-29"
  data
}
df2 = give_attr(df1)

# Problem: the original Series also gets the attribute while it shouldn't!
attributes(df1)
```

    #> $class
    #> [1] "RPolarsSeries"
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
df1 = as_polars_series(1:10)
df2 = give_attr(df1)

# now, the original Series doesn't get this attribute
attributes(df1)
```

    #> $class
    #> [1] "RPolarsSeries"
