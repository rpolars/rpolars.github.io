

# Drop duplicated rows

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L526)

## Description

Drop duplicated rows

## Usage

<pre><code class='language-R'>DataFrame_unique(subset = NULL, ..., keep = "any", maintain_order = FALSE)
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
<code id="DataFrame_unique_:_...">…</code>
</td>
<td>
Not used.
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

<code>“any”</code> (default): Does not give any guarantee of which row
is kept. This allows more optimizations.

</li>
<li>

<code>“first”</code>: Keep first unique row.

</li>
<li>

<code>“last”</code>: Keep last unique row.

</li>
<li>

<code>“none”</code>: Don’t keep duplicate rows.

</li>
</ul>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_unique_:_maintain_order">maintain_order</code>
</td>
<td>
Keep the same order as the original data. Setting this to
<code>TRUE</code> makes it more expensive to compute and blocks the
possibility to run on the streaming engine.
</td>
</tr>
</table>

## Value

DataFrame

## Examples

``` r
library(polars)

df = pl$DataFrame(
  x = c(1:3, 1:3, 3:1, 1L),
  y = c(1:3, 1:3, 1:3, 1L)
)
df$height
```

    #> [1] 10

``` r
df$unique()$height
```

    #> [1] 5

``` r
# subset to define unique, keep only last or first
df$unique(subset = "x", keep = "last")
```

    #> shape: (3, 2)
    #> ┌─────┬─────┐
    #> │ x   ┆ y   │
    #> │ --- ┆ --- │
    #> │ i32 ┆ i32 │
    #> ╞═════╪═════╡
    #> │ 3   ┆ 1   │
    #> │ 1   ┆ 1   │
    #> │ 2   ┆ 2   │
    #> └─────┴─────┘

``` r
df$unique(subset = "x", keep = "first")
```

    #> shape: (3, 2)
    #> ┌─────┬─────┐
    #> │ x   ┆ y   │
    #> │ --- ┆ --- │
    #> │ i32 ┆ i32 │
    #> ╞═════╪═════╡
    #> │ 3   ┆ 3   │
    #> │ 2   ┆ 2   │
    #> │ 1   ┆ 1   │
    #> └─────┴─────┘

``` r
# only keep unique rows
df$unique(keep = "none")
```

    #> shape: (2, 2)
    #> ┌─────┬─────┐
    #> │ x   ┆ y   │
    #> │ --- ┆ --- │
    #> │ i32 ┆ i32 │
    #> ╞═════╪═════╡
    #> │ 3   ┆ 1   │
    #> │ 1   ┆ 3   │
    #> └─────┴─────┘
