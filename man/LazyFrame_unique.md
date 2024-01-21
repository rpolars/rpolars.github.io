
# Drop duplicated rows

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L1022)

## Description

Drop duplicated rows

## Usage

<pre><code class='language-R'>LazyFrame_unique(subset = NULL, keep = "first", maintain_order = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_unique_:_subset">subset</code>
</td>
<td>
A character vector with the names of the column(s) to use to identify
duplicates. If <code>NULL</code> (default), use all columns.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_unique_:_keep">keep</code>
</td>
<td>

Which of the duplicate rows to keep:

<ul>
<li>

"first": Keep first unique row.

</li>
<li>

"last": Keep last unique row.

</li>
<li>

"none": Don’t keep duplicate rows.

</li>
</ul>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_unique_:_maintain_order">maintain_order</code>
</td>
<td>
Keep the same order as the original <code>DataFrame</code>. Setting this
to <code>TRUE</code> makes it more expensive to compute and blocks the
possibility to run on the streaming engine. The default value can be
changed with <code>pl$set_options(maintain_order = TRUE)</code>.
</td>
</tr>
</table>

## Value

LazyFrame

## Examples

``` r
library(polars)

df = pl$LazyFrame(
  x = sample(10, 100, rep = TRUE),
  y = sample(10, 100, rep = TRUE)
)
df$collect()$height
```

    #> [1] 100

``` r
df$unique()$collect()$height
```

    #> [1] 64

``` r
df$unique(subset = "x")$collect()$height
```

    #> [1] 10

``` r
df$unique(keep = "last")
```

    #> [1] "polars LazyFrame naive plan: (run ldf$describe_optimized_plan() to see the optimized plan)"
    #> UNIQUE BY None
    #>   DF ["x", "y"]; PROJECT */2 COLUMNS; SELECTION: "None"

``` r
# only keep unique rows
df$unique(keep = "none")
```

    #> [1] "polars LazyFrame naive plan: (run ldf$describe_optimized_plan() to see the optimized plan)"
    #> UNIQUE BY None
    #>   DF ["x", "y"]; PROJECT */2 COLUMNS; SELECTION: "None"
