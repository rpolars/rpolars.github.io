

# Get a slice of an Expr

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L1234)

## Description

Performing a slice of length 1 on a subset of columns will recycle this
value in those columns but will not change the number of rows in the
data. See examples.

## Usage

<pre><code class='language-R'>Expr_slice(offset, length = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_slice_:_offset">offset</code>
</td>
<td>
Numeric or expression, zero-indexed. Indicates where to start the slice.
A negative value is one-indexed and starts from the end.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_slice_:_length">length</code>
</td>
<td>
Maximum number of elements contained in the slice. Default is full data.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)


# as head
pl$DataFrame(list(a = 0:100))$select(
  pl$all()$slice(0, 6)
)
```

    #> shape: (6, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ i32 │
    #> ╞═════╡
    #> │ 0   │
    #> │ 1   │
    #> │ 2   │
    #> │ 3   │
    #> │ 4   │
    #> │ 5   │
    #> └─────┘

``` r
# as tail
pl$DataFrame(list(a = 0:100))$select(
  pl$all()$slice(-6, 6)
)
```

    #> shape: (6, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ i32 │
    #> ╞═════╡
    #> │ 95  │
    #> │ 96  │
    #> │ 97  │
    #> │ 98  │
    #> │ 99  │
    #> │ 100 │
    #> └─────┘

``` r
pl$DataFrame(list(a = 0:100))$select(
  pl$all()$slice(80)
)
```

    #> shape: (21, 1)
    #> ┌─────┐
    #> │ a   │
    #> │ --- │
    #> │ i32 │
    #> ╞═════╡
    #> │ 80  │
    #> │ 81  │
    #> │ 82  │
    #> │ 83  │
    #> │ 84  │
    #> │ …   │
    #> │ 96  │
    #> │ 97  │
    #> │ 98  │
    #> │ 99  │
    #> │ 100 │
    #> └─────┘

``` r
# recycling
pl$DataFrame(mtcars)$with_columns(pl$col("mpg")$slice(0, 1))
```

    #> shape: (32, 11)
    #> ┌──────┬─────┬───────┬───────┬───┬─────┬─────┬──────┬──────┐
    #> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
    #> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
    #> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
    #> ╞══════╪═════╪═══════╪═══════╪═══╪═════╪═════╪══════╪══════╡
    #> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
    #> │ 21.0 ┆ 6.0 ┆ 160.0 ┆ 110.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
    #> │ 21.0 ┆ 4.0 ┆ 108.0 ┆ 93.0  ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 1.0  │
    #> │ 21.0 ┆ 6.0 ┆ 258.0 ┆ 110.0 ┆ … ┆ 1.0 ┆ 0.0 ┆ 3.0  ┆ 1.0  │
    #> │ 21.0 ┆ 8.0 ┆ 360.0 ┆ 175.0 ┆ … ┆ 0.0 ┆ 0.0 ┆ 3.0  ┆ 2.0  │
    #> │ …    ┆ …   ┆ …     ┆ …     ┆ … ┆ …   ┆ …   ┆ …    ┆ …    │
    #> │ 21.0 ┆ 4.0 ┆ 95.1  ┆ 113.0 ┆ … ┆ 1.0 ┆ 1.0 ┆ 5.0  ┆ 2.0  │
    #> │ 21.0 ┆ 8.0 ┆ 351.0 ┆ 264.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 4.0  │
    #> │ 21.0 ┆ 6.0 ┆ 145.0 ┆ 175.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 6.0  │
    #> │ 21.0 ┆ 8.0 ┆ 301.0 ┆ 335.0 ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 8.0  │
    #> │ 21.0 ┆ 4.0 ┆ 121.0 ┆ 109.0 ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 2.0  │
    #> └──────┴─────┴───────┴───────┴───┴─────┴─────┴──────┴──────┘
