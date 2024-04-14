

# Create an empty or n-row null-filled copy of the LazyFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L2069)

## Description

Returns a n-row null-filled LazyFrame with an identical schema.
<code>n</code> can be greater than the current number of rows in the
LazyFrame.

## Usage

<pre><code class='language-R'>LazyFrame_clear(n = 0)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_clear_:_n">n</code>
</td>
<td>
Number of (null-filled) rows to return in the cleared frame.
</td>
</tr>
</table>

## Value

A n-row null-filled LazyFrame with an identical schema

## Examples

``` r
library(polars)

df = pl$LazyFrame(
  a = c(NA, 2, 3, 4),
  b = c(0.5, NA, 2.5, 13),
  c = c(TRUE, TRUE, FALSE, NA)
)

df$clear()
```

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #> DF ["a", "b", "c"]; PROJECT */3 COLUMNS; SELECTION: "None"

``` r
df$clear(n = 5)
```

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #> DF ["a", "b", "c"]; PROJECT */3 COLUMNS; SELECTION: "None"
