
# Drop duplicated rows

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L409)

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
    #> │ 6   ┆ 6   │
    #> │ 2   ┆ 4   │
    #> │ 1   ┆ 7   │
    #> │ 3   ┆ 9   │
    #> │ …   ┆ …   │
    #> │ 8   ┆ 5   │
    #> │ 10  ┆ 8   │
    #> │ 3   ┆ 4   │
    #> │ 9   ┆ 2   │
    #> └─────┴─────┘

``` r
# only keep unique rows
df$unique(keep = "none")
```

    #> shape: (42, 2)
    #> ┌─────┬─────┐
    #> │ x   ┆ y   │
    #> │ --- ┆ --- │
    #> │ i32 ┆ i32 │
    #> ╞═════╪═════╡
    #> │ 10  ┆ 10  │
    #> │ 2   ┆ 6   │
    #> │ 1   ┆ 9   │
    #> │ 5   ┆ 8   │
    #> │ …   ┆ …   │
    #> │ 9   ┆ 2   │
    #> │ 3   ┆ 7   │
    #> │ 8   ┆ 7   │
    #> │ 3   ┆ 3   │
    #> └─────┴─────┘
