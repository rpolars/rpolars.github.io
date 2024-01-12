
# Rechunk a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L1077)

## Description

Rechunking re-allocates any "chunked" memory allocations to speed-up
e.g. vectorized operations.

## Usage

<pre><code class='language-R'>DataFrame_rechunk()
</code></pre>

## Details

A DataFrame is a vector of Series. Each Series in rust-polars is a
wrapper around a ChunkedArray, which is like a virtual contiguous vector
physically backed by an ordered set of chunks. Each chunk of values has
a contiguous memory layout and is an arrow array. Arrow arrays are a
fast, thread-safe and cross-platform memory layout.

In R, combining with <code>c()</code> or <code>rbind()</code> requires
immediate vector re-allocation to place vector values in contiguous
memory. This is slow and memory consuming, and it is why repeatedly
appending to a vector in R is discouraged.

In polars, when we concatenate or append to Series or DataFrame, the
re-allocation can be avoided or delayed by simply appending chunks to
each individual Series. However, if chunks become many and small or are
misaligned across Series, this can hurt the performance of subsequent
operations.

Most places in the polars api where chunking could occur, the user have
to typically actively opt-out by setting an argument <code>rechunk =
FALSE</code>.

## Value

A DataFrame

## See Also

<code>\<DataFrame\>$n_chunks()</code>

## Examples

``` r
library(polars)

# create DataFrame with misaligned chunks
df = pl$concat(
  1:10, # single chunk
  pl$concat(1:5, 1:5, rechunk = FALSE, how = "vertical")$rename("b"), # two chunks
  how = "horizontal"
)
df
```

    #> shape: (10, 2)
    #> ┌─────┬─────┐
    #> │ x   ┆ b   │
    #> │ --- ┆ --- │
    #> │ i32 ┆ i32 │
    #> ╞═════╪═════╡
    #> │ 1   ┆ 1   │
    #> │ 2   ┆ 2   │
    #> │ 3   ┆ 3   │
    #> │ 4   ┆ 4   │
    #> │ …   ┆ …   │
    #> │ 7   ┆ 2   │
    #> │ 8   ┆ 3   │
    #> │ 9   ┆ 4   │
    #> │ 10  ┆ 5   │
    #> └─────┴─────┘

``` r
df$n_chunks()
```

    #> [1] 1 2

``` r
# rechunk a chunked DataFrame
df$rechunk()$n_chunks()
```

    #> [1] 1 1

``` r
# rechunk is not an in-place operation
df$n_chunks()
```

    #> [1] 1 2

``` r
# The following toy example emulates the Series "chunkyness" in R. Here it a
# S3-classed list with same type of vectors and where have all relevant S3
# generics implemented to make behave as if it was a regular vector.
"+.chunked_vector" = \(x, y) structure(list(unlist(x) + unlist(y)), class = "chunked_vector")
print.chunked_vector = \(x, ...) print(unlist(x), ...)
c.chunked_vector = \(...) {
  structure(do.call(c, lapply(list(...), unclass)), class = "chunked_vector")
}
rechunk = \(x) structure(unlist(x), class = "chunked_vector")
x = structure(list(1:4, 5L), class = "chunked_vector")
x
```

    #> [1] 1 2 3 4 5

``` r
x + 5:1
```

    #> [1] 6 6 6 6 6

``` r
lapply(x, tracemem) # trace chunks to verify no re-allocation
```

    #> [[1]]
    #> [1] "<0x55ca60280158>"
    #> 
    #> [[2]]
    #> [1] "<0x55ca5d18ea58>"

``` r
z = c(x, x)
z # looks like a plain vector
```

    #>  [1] 1 2 3 4 5 1 2 3 4 5

``` r
lapply(z, tracemem) # mem allocation  in z are the same from x
```

    #> [[1]]
    #> [1] "<0x55ca60280158>"
    #> 
    #> [[2]]
    #> [1] "<0x55ca5d18ea58>"
    #> 
    #> [[3]]
    #> [1] "<0x55ca60280158>"
    #> 
    #> [[4]]
    #> [1] "<0x55ca5d18ea58>"

``` r
str(z)
```

    #> List of 4
    #>  $ : int [1:4] 1 2 3 4
    #>  $ : int 5
    #>  $ : int [1:4] 1 2 3 4
    #>  $ : int 5
    #>  - attr(*, "class")= chr "chunked_vector"

``` r
z = rechunk(z)
str(z)
```

    #>  'chunked_vector' int [1:10] 1 2 3 4 5 1 2 3 4 5
