

# Return the first or the last <code>n</code> parts of an object

## Description

They are equivalent to <code style="white-space: pre;">$head()</code>
and <code style="white-space: pre;">$tail()</code> methods.

## Usage

<pre><code class='language-R'>## S3 method for class 'RPolarsDataFrame'
head(x, n = 6L, ...)

# S3 method for class 'RPolarsLazyFrame'
head(x, n = 6L, ...)

# S3 method for class 'RPolarsDataFrame'
tail(x, n = 6L, ...)

# S3 method for class 'RPolarsLazyFrame'
tail(x, n = 6L, ...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="x">x</code>
</td>
<td>
A polars object
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="n">n</code>
</td>
<td>
An integer vector of length 1. Note that negative values are not
supported for if <code>x</code> is a LazyFrame.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="...">…</code>
</td>
<td>
Ignored
</td>
</tr>
</table>

## Value

A polars object of the same class as <code>x</code>

## See Also

<ul>
<li>

<code>\<DataFrame\>$head()</code>

</li>
<li>

<code>\<LazyFrame\>$head()</code>

</li>
<li>

<code>\<DataFrame\>$tail()</code>

</li>
<li>

<code>\<LazyFrame\>$tail()</code>

</li>
<li>

<code>\<LazyFrame\>$fetch()</code>

</li>
</ul>

## Examples

``` r
library(polars)

df = pl$DataFrame(foo = 1:5, bar = 6:10, ham = letters[1:5])
lf = df$lazy()

head(df, 2)
```

    #> shape: (2, 3)
    #> ┌─────┬─────┬─────┐
    #> │ foo ┆ bar ┆ ham │
    #> │ --- ┆ --- ┆ --- │
    #> │ i32 ┆ i32 ┆ str │
    #> ╞═════╪═════╪═════╡
    #> │ 1   ┆ 6   ┆ a   │
    #> │ 2   ┆ 7   ┆ b   │
    #> └─────┴─────┴─────┘

``` r
tail(df, 2)
```

    #> shape: (2, 3)
    #> ┌─────┬─────┬─────┐
    #> │ foo ┆ bar ┆ ham │
    #> │ --- ┆ --- ┆ --- │
    #> │ i32 ┆ i32 ┆ str │
    #> ╞═════╪═════╪═════╡
    #> │ 4   ┆ 9   ┆ d   │
    #> │ 5   ┆ 10  ┆ e   │
    #> └─────┴─────┴─────┘

``` r
head(lf, 2)
```

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #> SLICE[offset: 0, len: 2]
    #>   DF ["foo", "bar", "ham"]; PROJECT */3 COLUMNS; SELECTION: "None"

``` r
tail(lf, 2)
```

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #> SLICE[offset: -2, len: 2]
    #>   DF ["foo", "bar", "ham"]; PROJECT */3 COLUMNS; SELECTION: "None"

``` r
head(df, -2)
```

    #> shape: (3, 3)
    #> ┌─────┬─────┬─────┐
    #> │ foo ┆ bar ┆ ham │
    #> │ --- ┆ --- ┆ --- │
    #> │ i32 ┆ i32 ┆ str │
    #> ╞═════╪═════╪═════╡
    #> │ 1   ┆ 6   ┆ a   │
    #> │ 2   ┆ 7   ┆ b   │
    #> │ 3   ┆ 8   ┆ c   │
    #> └─────┴─────┴─────┘

``` r
tail(df, -2)
```

    #> shape: (3, 3)
    #> ┌─────┬─────┬─────┐
    #> │ foo ┆ bar ┆ ham │
    #> │ --- ┆ --- ┆ --- │
    #> │ i32 ┆ i32 ┆ str │
    #> ╞═════╪═════╪═════╡
    #> │ 3   ┆ 8   ┆ c   │
    #> │ 4   ┆ 9   ┆ d   │
    #> │ 5   ┆ 10  ┆ e   │
    #> └─────┴─────┴─────┘
