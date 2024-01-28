

# Cast between DataType

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/expr__expr.R#L1019)

## Description

Cast between DataType

## Usage

<pre><code class='language-R'>Expr_cast(dtype, strict = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_cast_:_dtype">dtype</code>
</td>
<td>
DataType to cast to.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_cast_:_strict">strict</code>
</td>
<td>
If <code>TRUE</code> (default), an error will be thrown if cast failed
at resolve time.
</td>
</tr>
</table>

## Value

Expr

## Examples

``` r
library(polars)

df = pl$DataFrame(a = 1:3, b = c(1, 2, 3))
df$with_columns(
  pl$col("a")$cast(pl$dtypes$Float64),
  pl$col("b")$cast(pl$dtypes$Int32)
)
```

    #> shape: (3, 2)
    #> ┌─────┬─────┐
    #> │ a   ┆ b   │
    #> │ --- ┆ --- │
    #> │ f64 ┆ i32 │
    #> ╞═════╪═════╡
    #> │ 1.0 ┆ 1   │
    #> │ 2.0 ┆ 2   │
    #> │ 3.0 ┆ 3   │
    #> └─────┴─────┘

``` r
# strict FALSE, inserts null for any cast failure
pl$lit(c(100, 200, 300))$cast(pl$dtypes$UInt8, strict = FALSE)$to_series()
```

    #> polars Series: shape: (3,)
    #> Series: '' [u8]
    #> [
    #>  100
    #>  200
    #>  null
    #> ]

``` r
# strict TRUE, raise any failure as an error when query is executed.
tryCatch(
  {
    pl$lit("a")$cast(pl$dtypes$Float64, strict = TRUE)$to_series()
  },
  error = function(e) e
)
```

    #> <RPolarsErr_error: Execution halted with the following contexts
    #>    0: In R: in $select()
    #>    0: During function call [.main()]
    #>    1: Encountered the following error in Rust-Polars:
    #>          cannot cast non numeric any-value to numeric dtype
    #> >
