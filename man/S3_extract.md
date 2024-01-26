

# Extract Parts of a Polars Object

## Description

Mimics the behavior of \[<code>x\[i, j, drop =
TRUE\]</code>\]\[Extract\] for data.frame or R vector.

## Usage

<pre><code class='language-R'>## S3 method for class 'RPolarsDataFrame'
x[i, j, drop = TRUE]

# S3 method for class 'RPolarsLazyFrame'
x[i, j, drop = TRUE]

# S3 method for class 'RPolarsSeries'
x[i]
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="+5B.RPolarsDataFrame_:_x">x</code>
</td>
<td>
A DataFrame, LazyFrame, or Series
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="+5B.RPolarsDataFrame_:_i">i</code>
</td>
<td>
Rows to select. Integer vector, logical vector, or an Expression.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="+5B.RPolarsDataFrame_:_j">j</code>
</td>
<td>
Columns to select. Integer vector, logical vector, character vector, or
an Expression. For LazyFrames, only an Expression can be used.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="+5B.RPolarsDataFrame_:_drop">drop</code>
</td>
<td>
Convert to a Polars Series if only one column is selected. For
LazyFrames, if the result has one column and <code>drop = TRUE</code>,
an error will occur.
</td>
</tr>
</table>

## Details

<code style="white-space: pre;">\<Series\>\[i\]</code> is equivalent to
<code style="white-space: pre;">pl$select(\<Series\>)\[i, , drop =
TRUE\]</code>.

## See Also

<code>\<DataFrame\>$select()</code>,
<code>\<LazyFrame\>$select()</code>,
<code>\<DataFrame\>$filter()</code>, <code>\<LazyFrame\>$filter()</code>

## Examples

``` r
library(polars)

df = pl$DataFrame(data.frame(a = 1:3, b = letters[1:3]))
lf = df$lazy()

# Select a row
df[1, ]
```

    #> shape: (1, 2)
    #> ┌─────┬─────┐
    #> │ a   ┆ b   │
    #> │ --- ┆ --- │
    #> │ i32 ┆ str │
    #> ╞═════╪═════╡
    #> │ 1   ┆ a   │
    #> └─────┴─────┘

``` r
# If only `i` is specified, it is treated as `j`
# Select a column
df[1]
```

    #> shape: (3, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ i32 │
    #> ╞═════╡
    #> │ 1   │
    #> │ 2   │
    #> │ 3   │
    #> └─────┘

``` r
# Select a column by name (and convert to a Series)
df[, "b"]
```

    #> polars Series: shape: (3,)
    #> Series: 'b' [str]
    #> [
    #>  "a"
    #>  "b"
    #>  "c"
    #> ]

``` r
# Can use Expression for filtering and column selection
lf[pl$col("a") >= 2, pl$col("b")$alias("new"), drop = FALSE] |>
  as.data.frame()
```

    #>   new
    #> 1   b
    #> 2   c
