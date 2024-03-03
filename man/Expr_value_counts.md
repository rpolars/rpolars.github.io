

# Value counts

[**Source code**](https://github.com/pola-rs/r-polars/tree/97c09bc0a6fc3d166744dbddd037b49e8d8fc6c2/R/expr__expr.R#L3110)

## Description

Count all unique values and create a struct mapping value to count.

## Usage

<pre><code class='language-R'>Expr_value_counts(sort = FALSE, parallel = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_value_counts_:_sort">sort</code>
</td>
<td>
Ensure the output is sorted from most values to least.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_value_counts_:_parallel">parallel</code>
</td>
<td>
Better to turn this off in the aggregation context, as it can lead to
contention.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(iris)$select(pl$col("Species")$value_counts())
df
```

    #> shape: (3, 1)
    #> ┌───────────────────┐
    #> │ Species           │
    #> │ ---               │
    #> │ struct[2]         │
    #> ╞═══════════════════╡
    #> │ {"setosa",50}     │
    #> │ {"versicolor",50} │
    #> │ {"virginica",50}  │
    #> └───────────────────┘

``` r
df$unnest()$to_data_frame() # recommended to unnest structs before converting to R
```

    #>      Species count
    #> 1     setosa    50
    #> 2 versicolor    50
    #> 3  virginica    50
