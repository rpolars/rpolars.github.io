

# Drop duplicated rows

## Description

Drop duplicated rows

## Usage

<pre><code class='language-R'>## S3 method for class 'RPolarsDataFrame'
unique(x, incomparables = FALSE, subset = NULL, keep = "first", ...)

# S3 method for class 'RPolarsLazyFrame'
unique(x, incomparables = FALSE, subset = NULL, keep = "first", ...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="unique.RPolarsDataFrame_:_x">x</code>
</td>
<td>
A DataFrame or LazyFrame
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="unique.RPolarsDataFrame_:_incomparables">incomparables</code>
</td>
<td>
Not used.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="unique.RPolarsDataFrame_:_subset">subset</code>
</td>
<td>
Character vector of column names to drop duplicated values from.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="unique.RPolarsDataFrame_:_keep">keep</code>
</td>
<td>
Either <code>“first”</code>, <code>“last”</code>, or
<code>“none”</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="unique.RPolarsDataFrame_:_...">…</code>
</td>
<td>
Not used.
</td>
</tr>
</table>

## Examples

``` r
library(polars)

df = pl$DataFrame(
  x = as.numeric(c(1, 1:5)),
  y = as.numeric(c(1, 1:5)),
  z = as.numeric(c(1, 1, 1:4))
)
unique(df)
```

    #> shape: (5, 3)
    #> ┌─────┬─────┬─────┐
    #> │ x   ┆ y   ┆ z   │
    #> │ --- ┆ --- ┆ --- │
    #> │ f64 ┆ f64 ┆ f64 │
    #> ╞═════╪═════╪═════╡
    #> │ 1.0 ┆ 1.0 ┆ 1.0 │
    #> │ 2.0 ┆ 2.0 ┆ 1.0 │
    #> │ 3.0 ┆ 3.0 ┆ 2.0 │
    #> │ 5.0 ┆ 5.0 ┆ 4.0 │
    #> │ 4.0 ┆ 4.0 ┆ 3.0 │
    #> └─────┴─────┴─────┘
