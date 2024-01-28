

# Ungroup a RollingGroupBy object

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/group_by_rolling.R#L124)

## Description

Revert the <code style="white-space: pre;">$rolling()</code> operation.
Doing
<code style="white-space: pre;">\<DataFrame\>$rolling(…)$ungroup()</code>
returns the original <code>DataFrame</code>.

## Usage

<pre><code class='language-R'>RollingGroupBy_ungroup()
</code></pre>

## Value

DataFrame

## Examples

``` r
library(polars)

df = pl$DataFrame(
  dt = c("2020-01-01", "2020-01-01", "2020-01-01", "2020-01-02", "2020-01-03", "2020-01-08"),
  a = c(3, 7, 5, 9, 2, 1)
)$with_columns(
  pl$col("dt")$str$strptime(pl$Date, format = NULL)$set_sorted()
)

df$rolling(index_column = "dt", period = "2d")$ungroup()
```

    #> shape: (6, 2)
    #> ┌────────────┬─────┐
    #> │ dt         ┆ a   │
    #> │ ---        ┆ --- │
    #> │ date       ┆ f64 │
    #> ╞════════════╪═════╡
    #> │ 2020-01-01 ┆ 3.0 │
    #> │ 2020-01-01 ┆ 7.0 │
    #> │ 2020-01-01 ┆ 5.0 │
    #> │ 2020-01-02 ┆ 9.0 │
    #> │ 2020-01-03 ┆ 2.0 │
    #> │ 2020-01-08 ┆ 1.0 │
    #> └────────────┴─────┘
