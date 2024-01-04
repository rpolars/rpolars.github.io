
# Get r vector/list

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L278)

## Description

return R list (if polars Series is list) or vector (any other polars
Series type)

return R vector (implicit unlist)

return R list (implicit as.list)

## Usage

<pre><code class='language-R'>Series_to_r()

Series_to_vector()

Series_to_r_list()
</code></pre>

## Details

Fun fact: Nested polars Series list must have same inner type,
e.g. List(List(Int32)) Thus every leaf(non list type) will be placed on
the same depth of the tree, and be the same type.

## Value

R list or vector

R vector

R list

## Examples

``` r
library(polars)


series_vec = pl$Series(letters[1:3])

# Series_non_list
series_vec$to_r() # as vector because Series DataType is not list (is String)
```

    #> [1] "a" "b" "c"

``` r
series_vec$to_r_list() # implicit call as.list(), convert to list
```

    #> [[1]]
    #> [1] "a"
    #> 
    #> [[2]]
    #> [1] "b"
    #> 
    #> [[3]]
    #> [1] "c"

``` r
series_vec$to_vector() # implicit call unlist(), same as to_r() as already vector
```

    #> [1] "a" "b" "c"

``` r
# make nested Series_list of Series_list of Series_Int32
# using Expr syntax because currently more complete translated
series_list = pl$DataFrame(list(a = c(1:5, NA_integer_)))$select(
  pl$col("a")$implode()$implode()$append(
    (
      pl$col("a")$head(2)$implode()$append(
        pl$col("a")$tail(1)$implode()
      )
    )$implode()
  )
)$get_column("a") # get series from DataFrame

# Series_list
series_list$to_r() # as list because Series DataType is list
```

    #> [[1]]
    #> [[1]][[1]]
    #> [1]  1  2  3  4  5 NA
    #> 
    #> 
    #> [[2]]
    #> [[2]][[1]]
    #> [1] 1 2
    #> 
    #> [[2]][[2]]
    #> [1] NA

``` r
series_list$to_r_list() # implicit call as.list(), same as to_r() as already list
```

    #> [[1]]
    #> [[1]][[1]]
    #> [1]  1  2  3  4  5 NA
    #> 
    #> 
    #> [[2]]
    #> [[2]][[1]]
    #> [1] 1 2
    #> 
    #> [[2]][[2]]
    #> [1] NA

``` r
series_list$to_vector() # implicit call unlist(), append into a vector
```

    #> [1]  1  2  3  4  5 NA  1  2 NA

``` r
#
```
