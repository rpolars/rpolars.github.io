
# Polars raw list

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__eager.R#L323)

## Description

Create an "rpolars_raw_list", which is an R list where all elements must
be an R raw or <code>NULL</code>.

## Usage

<pre><code class='language-R'>pl_raw_list(...)

# S3 method for class 'rpolars_raw_list'
x[index]

# S3 method for class 'rpolars_raw_list'
as.list(x, ...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_raw_list_:_...">…</code>
</td>
<td>
Elements
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_raw_list_:_x">x</code>
</td>
<td>
A <code>rpolars_raw_list</code> object created with
<code>pl$raw_list()</code>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_raw_list_:_index">index</code>
</td>
<td>
Elements to select
</td>
</tr>
</table>

## Details

In R, raw can contain a binary sequence of bytes, and the length is the
number of bytes. In polars a Series of DataType Binary is more like a
vector of vectors of bytes where missing values are allowed, similar to
how <code>NA</code>s can be present in vectors.

To ensure correct round-trip conversion, r-polars uses an R list where
any elements must be raw or <code>NULL</code> (encoded as missing), and
the S3 class is <code>c(“rpolars_raw_list”,“list”)</code>.

## Value

An R list where any elements must be raw, and the S3 class is
<code>c(“rpolars_raw_list”,“list”)</code>.

## Examples

``` r
library(polars)

# create a rpolars_raw_list
raw_list = pl$raw_list(raw(1), raw(3), charToRaw("alice"), NULL)

# pass it to Series or lit
pl$Series(raw_list)
```

    #> polars Series: shape: (4,)
    #> Series: '' [binary]
    #> [
    #>  [binary data]
    #>  [binary data]
    #>  [binary data]
    #>  null
    #> ]

``` r
pl$lit(raw_list)
```

    #> polars Expr: Series

``` r
# convert polars bianry Series to rpolars_raw_list
pl$Series(raw_list)$to_r()
```

    #> [[1]]
    #> [1] 00
    #> 
    #> [[2]]
    #> [1] 00 00 00
    #> 
    #> [[3]]
    #> [1] 61 6c 69 63 65
    #> 
    #> [[4]]
    #> NULL
    #> 
    #> attr(,"class")
    #> [1] "rpolars_raw_list" "list"

``` r
# NB: a plain list of raws yield a polars Series of DateType [list[Binary]]
# which is not the same
pl$Series(list(raw(1), raw(2)))
```

    #> polars Series: shape: (2,)
    #> Series: '' [list[binary]]
    #> [
    #>  [[binary data]]
    #>  [[binary data]]
    #> ]

``` r
# to regular list, use as.list or unclass
as.list(raw_list)
```

    #> [[1]]
    #> [1] 00
    #> 
    #> [[2]]
    #> [1] 00 00 00
    #> 
    #> [[3]]
    #> [1] 61 6c 69 63 65
    #> 
    #> [[4]]
    #> NULL

``` r
# subsetting preserves class
pl$raw_list(NULL, raw(2), raw(3))[1:2]
```

    #> [[1]]
    #> NULL
    #> 
    #> [[2]]
    #> [1] 00 00
    #> 
    #> attr(,"class")
    #> [1] "rpolars_raw_list" "list"

``` r
# to regular list, use as.list or unclass
pl$raw_list(NULL, raw(2), raw(3)) |> as.list()
```

    #> [[1]]
    #> NULL
    #> 
    #> [[2]]
    #> [1] 00 00
    #> 
    #> [[3]]
    #> [1] 00 00 00
