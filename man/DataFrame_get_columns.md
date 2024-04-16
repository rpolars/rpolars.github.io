

# Get the DataFrame as a List of Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/741f9cd2614b3302a4d033bcae447425e1b91191/R/after-wrappers.R#L20)

## Description

Get the DataFrame as a List of Series

## Usage

<pre><code class='language-R'>DataFrame_get_columns()
</code></pre>

## Value

A list of Series

## See Also

<ul>
<li>

<code>\<DataFrame\>$to_list()</code>: Similar to this method but returns
a list of vectors instead of Series.

</li>
</ul>

## Examples

``` r
library(polars)

df = pl$DataFrame(foo = 1L:3L, bar = 4L:6L)
df$get_columns()
```

    #> [[1]]
    #> polars Series: shape: (3,)
    #> Series: 'foo' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #> ]
    #> 
    #> [[2]]
    #> polars Series: shape: (3,)
    #> Series: 'bar' [i32]
    #> [
    #>  4
    #>  5
    #>  6
    #> ]

``` r
df = pl$DataFrame(
  a = 1:4,
  b = c(0.5, 4, 10, 13),
  c = c(TRUE, TRUE, FALSE, TRUE)
)
df$get_columns()
```

    #> [[1]]
    #> polars Series: shape: (4,)
    #> Series: 'a' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #>  4
    #> ]
    #> 
    #> [[2]]
    #> polars Series: shape: (4,)
    #> Series: 'b' [f64]
    #> [
    #>  0.5
    #>  4.0
    #>  10.0
    #>  13.0
    #> ]
    #> 
    #> [[3]]
    #> polars Series: shape: (4,)
    #> Series: 'c' [bool]
    #> [
    #>  true
    #>  true
    #>  false
    #>  true
    #> ]
