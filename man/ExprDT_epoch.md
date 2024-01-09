
# Epoch

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__datetime.R#L553)

## Description

Get the time passed since the Unix EPOCH in the give time unit.

## Usage

<pre><code class='language-R'>ExprDT_epoch(tu = c("us", "ns", "ms", "s", "d"))
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprDT_epoch_:_tu">tu</code>
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

pl$date_range(as.Date("2022-1-1"), eager = FALSE)$dt$epoch("ns")$to_series()
```

    #> polars Series: shape: (1,)
    #> Series: '' [i64]
    #> [
    #>  1640995200000000000
    #> ]

``` r
pl$date_range(as.Date("2022-1-1"), eager = FALSE)$dt$epoch("ms")$to_series()
```

    #> polars Series: shape: (1,)
    #> Series: '' [i64]
    #> [
    #>  1640995200000
    #> ]

``` r
pl$date_range(as.Date("2022-1-1"), eager = FALSE)$dt$epoch("s")$to_series()
```

    #> polars Series: shape: (1,)
    #> Series: '' [i64]
    #> [
    #>  1640995200
    #> ]

``` r
pl$date_range(as.Date("2022-1-1"), eager = FALSE)$dt$epoch("d")$to_series()
```

    #> polars Series: shape: (1,)
    #> Series: '' [i32]
    #> [
    #>  18993
    #> ]
