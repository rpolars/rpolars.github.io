

# Generate a range of integers

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L1315)

## Description

Generate a range of integers

## Usage

<pre><code class='language-R'>pl_int_range(start = 0, end = NULL, step = 1, ..., dtype = pl\$Int64)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="start">start</code>
</td>
<td>
Start of the range (inclusive). Defaults to 0.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="end">end</code>
</td>
<td>
End of the range (exclusive). If <code>NULL</code> (default), the value
of <code>start</code> is used and <code>start</code> is set to 0.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="step">step</code>
</td>
<td>
Step size of the range.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="...">…</code>
</td>
<td>
Not used.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="dtype">dtype</code>
</td>
<td>
Data type of the range.
</td>
</tr>
</table>

## Value

An Expr with the data type specified in <code>dtype</code> (default is
<code>Int64</code>).

## See Also

<code>pl$int_ranges()</code> to generate a range of integers for each
row of the input columns.

## Examples

``` r
library(polars)

pl$int_range(0, 3) |>
  as_polars_series()
```

    #> polars Series: shape: (3,)
    #> Series: 'literal' [i64]
    #> [
    #>  0
    #>  1
    #>  2
    #> ]

``` r
# "end" can be omitted for shorter syntax
pl$int_range(3) |>
  as_polars_series()
```

    #> polars Series: shape: (3,)
    #> Series: 'literal' [i64]
    #> [
    #>  0
    #>  1
    #>  2
    #> ]

``` r
# custom data type
pl$int_range(3, dtype = pl$Int16) |>
  as_polars_series()
```

    #> polars Series: shape: (3,)
    #> Series: 'literal' [i16]
    #> [
    #>  0
    #>  1
    #>  2
    #> ]

``` r
# one can use pl$int_range() and pl$len() to create an index column
df = pl$DataFrame(a = c(1, 3, 5), b = c(2, 4, 6))
df$select(
  index = pl$int_range(pl$len(), dtype = pl$UInt32),
  pl$all()
)
```

    #> shape: (3, 3)
    #> ┌───────┬─────┬─────┐
    #> │ index ┆ a   ┆ b   │
    #> │ ---   ┆ --- ┆ --- │
    #> │ u32   ┆ f64 ┆ f64 │
    #> ╞═══════╪═════╪═════╡
    #> │ 0     ┆ 1.0 ┆ 2.0 │
    #> │ 1     ┆ 3.0 ┆ 4.0 │
    #> │ 2     ┆ 5.0 ┆ 6.0 │
    #> └───────┴─────┴─────┘
