

# Epoch

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/expr__datetime.R#L536)

## Description

Get the time passed since the Unix EPOCH in the give time unit.

## Usage

<pre><code class='language-R'>ExprDT_epoch(tu = c("us", "ns", "ms", "s", "d"))
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="tu">tu</code>
</td>
<td>
string option either ‘ns’, ‘us’, ‘ms’, ‘s’ or ‘d’
</td>
</tr>
</table>

## Details

ns and perhaps us will exceed integerish limit if returning to R as
flaot64/double.

## Value

Expr of epoch as UInt32

## Examples

``` r
library(polars)

as_polars_series(as.Date("2022-1-1"))$dt$epoch("ns")
```

    #> polars Series: shape: (1,)
    #> Series: '' [i64]
    #> [
    #>  1640995200000000000
    #> ]

``` r
as_polars_series(as.Date("2022-1-1"))$dt$epoch("ms")
```

    #> polars Series: shape: (1,)
    #> Series: '' [i64]
    #> [
    #>  1640995200000
    #> ]

``` r
as_polars_series(as.Date("2022-1-1"))$dt$epoch("s")
```

    #> polars Series: shape: (1,)
    #> Series: '' [i64]
    #> [
    #>  1640995200
    #> ]

``` r
as_polars_series(as.Date("2022-1-1"))$dt$epoch("d")
```

    #> polars Series: shape: (1,)
    #> Series: '' [i32]
    #> [
    #>  18993
    #> ]
