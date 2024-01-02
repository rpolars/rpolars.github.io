
# Drop duplicated rows

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/dataframe__frame.R#L409)

## Description

Drop duplicated rows

## Usage

<pre><code class='language-R'>DataFrame_unique(subset = NULL, keep = "first", maintain_order = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_unique_:_subset">subset</code>
</td>
<td>
A character vector with the names of the column(s) to use to identify
duplicates. If <code>NULL</code> (default), use all columns.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_unique_:_keep">keep</code>
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
<code id="DataFrame_unique_:_maintain_order">maintain_order</code>
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

DataFrame

## Examples

``` r
library(polars)

df = pl$DataFrame(
  x = sample(10, 100, rep = TRUE),
  y = sample(10, 100, rep = TRUE)
)
df$height
```

    #> [1] 100

``` r
df$unique()$height
```

    #> [1] 66

``` r
df$unique(subset = "x")$height
```

    #> [1] 10

``` r
df$unique(keep = "last")
```

    #> shape: (66, 2)
    #> ┌─────┬─────┐
    #> │ x   ┆ y   │
    #> │ --- ┆ --- │
    #> │ i32 ┆ i32 │
    #> ╞═════╪═════╡
    #> │ 10  ┆ 10  │
    #> │ 3   ┆ 4   │
    #> │ 9   ┆ 7   │
    #> │ 8   ┆ 6   │
    #> │ …   ┆ …   │
    #> │ 10  ┆ 7   │
    #> │ 4   ┆ 7   │
    #> │ 9   ┆ 8   │
    #> │ 6   ┆ 9   │
    #> └─────┴─────┘

``` r
# only keep unique rows
df$unique(keep = "none")
```

    #> shape: (39, 2)
    #> ┌─────┬─────┐
    #> │ x   ┆ y   │
    #> │ --- ┆ --- │
    #> │ i32 ┆ i32 │
    #> ╞═════╪═════╡
    #> │ 6   ┆ 7   │
    #> │ 6   ┆ 8   │
    #> │ 1   ┆ 2   │
    #> │ 9   ┆ 7   │
    #> │ …   ┆ …   │
    #> │ 9   ┆ 8   │
    #> │ 6   ┆ 1   │
    #> │ 6   ┆ 9   │
    #> │ 6   ┆ 2   │
    #> └─────┴─────┘
