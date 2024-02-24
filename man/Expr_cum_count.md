

# Cumulative count

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L1481)

## Description

Get an array with the cumulative count (zero-indexed) computed at every
element.

## Usage

<pre><code class='language-R'>Expr_cum_count(reverse = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_cum_count_:_reverse">reverse</code>
</td>
<td>
If <code>TRUE</code>, reverse the count.
</td>
</tr>
</table>

## Details

The Dtypes Int8, UInt8, Int16 and UInt16 are cast to Int64 before
summing to prevent overflow issues.

<code style="white-space: pre;">$cum_count()</code> does not seem to
count within lists.

## Value

Expr

## Examples

``` r
library(polars)

pl$DataFrame(a = 1:4)$with_columns(
  pl$col("a")$cum_count()$alias("cum_count"),
  pl$col("a")$cum_count(reverse = TRUE)$alias("cum_count_reversed")
)
```

    #> shape: (4, 3)
    #> ┌─────┬───────────┬────────────────────┐
    #> │ a   ┆ cum_count ┆ cum_count_reversed │
    #> │ --- ┆ ---       ┆ ---                │
    #> │ i32 ┆ u32       ┆ u32                │
    #> ╞═════╪═══════════╪════════════════════╡
    #> │ 1   ┆ 1         ┆ 4                  │
    #> │ 2   ┆ 2         ┆ 3                  │
    #> │ 3   ┆ 3         ┆ 2                  │
    #> │ 4   ┆ 4         ┆ 1                  │
    #> └─────┴───────────┴────────────────────┘
