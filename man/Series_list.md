

# list: list related methods on Series of dtype List

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L917)

## Description

Create an object namespace of all list related methods. See the
individual method pages for full details

## Usage

<pre><code class='language-R'>Series_list()
</code></pre>

## Value

Series

## Examples

``` r
library(polars)

s = pl$Series(list(1:3, 1:2, NULL))
s
```

    #> polars Series: shape: (3,)
    #> Series: '' [list[i32]]
    #> [
    #>  [1, 2, 3]
    #>  [1, 2]
    #>  []
    #> ]

``` r
s$list$first()
```

    #> shape: (3, 1)
    #> ┌──────┐
    #> │      │
    #> │ ---  │
    #> │ i32  │
    #> ╞══════╡
    #> │ 1    │
    #> │ 1    │
    #> │ null │
    #> └──────┘
