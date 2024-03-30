

# Generate a range of integers for each row of the input columns

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L1333)

## Description

Generate a range of integers for each row of the input columns

## Usage

<pre><code class='language-R'>pl_int_ranges(start = 0, end = NULL, step = 1, ..., dtype = pl\$Int64)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_int_ranges_:_start">start</code>
</td>
<td>
Start of the range (inclusive). Defaults to 0.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_int_ranges_:_end">end</code>
</td>
<td>
End of the range (exclusive). If <code>NULL</code> (default), the value
of <code>start</code> is used and <code>start</code> is set to 0.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_int_ranges_:_step">step</code>
</td>
<td>
Step size of the range.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_int_ranges_:_...">…</code>
</td>
<td>
Not used.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_int_ranges_:_dtype">dtype</code>
</td>
<td>
Data type of the range.
</td>
</tr>
</table>

## Value

An Expr with the data type List(<code>dtype</code>) (with
<code>Int64</code> as default of <code>dtype</code>).

## See Also

<code>pl$int_range()</code> to generate a single range of integers.

## Examples

``` r
library(polars)

df = pl$DataFrame(start = c(1, -1), end = c(3, 2))

df$with_columns(int_range = pl$int_ranges("start", "end"))
```

    #> shape: (2, 3)
    #> ┌───────┬─────┬────────────┐
    #> │ start ┆ end ┆ int_range  │
    #> │ ---   ┆ --- ┆ ---        │
    #> │ f64   ┆ f64 ┆ list[i64]  │
    #> ╞═══════╪═════╪════════════╡
    #> │ 1.0   ┆ 3.0 ┆ [1, 2]     │
    #> │ -1.0  ┆ 2.0 ┆ [-1, 0, 1] │
    #> └───────┴─────┴────────────┘

``` r
df$with_columns(int_range = pl$int_ranges("start", "end", dtype = pl$Int16))
```

    #> shape: (2, 3)
    #> ┌───────┬─────┬────────────┐
    #> │ start ┆ end ┆ int_range  │
    #> │ ---   ┆ --- ┆ ---        │
    #> │ f64   ┆ f64 ┆ list[i16]  │
    #> ╞═══════╪═════╪════════════╡
    #> │ 1.0   ┆ 3.0 ┆ [1, 2]     │
    #> │ -1.0  ┆ 2.0 ┆ [-1, 0, 1] │
    #> └───────┴─────┴────────────┘
