
# Series to DataFrame

## Description

Series to DataFrame

## Usage

<pre><code class='language-R'>Series_to_frame()
</code></pre>

## Format

method

## Value

Series

## Examples

``` r
library(polars)

pl$Series(1:4, "bob")$to_frame()
```

    #> shape: (4, 1)
    #> ┌─────┐
    #> │ bob │
    #> │ --- │
    #> │ i32 │
    #> ╞═════╡
    #> │ 1   │
    #> │ 2   │
    #> │ 3   │
    #> │ 4   │
    #> └─────┘
