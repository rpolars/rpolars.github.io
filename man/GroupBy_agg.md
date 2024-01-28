

# Aggregate over a GroupBy

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/group_by.R#L89)

## Description

Aggregate a DataFrame over a groupby

## Usage

<pre><code class='language-R'>GroupBy_agg(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="GroupBy_agg_:_...">…</code>
</td>
<td>
exprs to aggregate over. … args can also be passed wrapped in a list
<code style="white-space: pre;">$agg(list(e1,e2,e3))</code>
</td>
</tr>
</table>

## Value

aggregated DataFrame

## Examples

``` r
library(polars)

pl$DataFrame(
  foo = c("one", "two", "two", "one", "two"),
  bar = c(5, 3, 2, 4, 1)
)$
  group_by("foo")$
  agg(
  pl$col("bar")$sum()$name$suffix("_sum"),
  pl$col("bar")$mean()$alias("bar_tail_sum")
)
```

    #> shape: (2, 3)
    #> ┌─────┬─────────┬──────────────┐
    #> │ foo ┆ bar_sum ┆ bar_tail_sum │
    #> │ --- ┆ ---     ┆ ---          │
    #> │ str ┆ f64     ┆ f64          │
    #> ╞═════╪═════════╪══════════════╡
    #> │ one ┆ 9.0     ┆ 4.5          │
    #> │ two ┆ 6.0     ┆ 2.0          │
    #> └─────┴─────────┴──────────────┘
