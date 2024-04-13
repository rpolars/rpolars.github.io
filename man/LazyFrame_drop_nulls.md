

# Drop nulls (missing values)

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/lazyframe__lazy.R#L1132)

## Description

Drop all rows that contain nulls (which correspond to <code>NA</code> in
R).

## Usage

<pre><code class='language-R'>LazyFrame_drop_nulls(subset = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_drop_nulls_:_subset">subset</code>
</td>
<td>
A character vector with the names of the column(s) for which nulls are
considered. If <code>NULL</code> (default), use all columns.
</td>
</tr>
</table>

## Value

LazyFrame

## Examples

``` r
library(polars)

tmp = mtcars
tmp[1:3, "mpg"] = NA
tmp[4, "hp"] = NA
tmp = pl$LazyFrame(tmp)

# number of rows in `tmp` before dropping nulls
tmp$collect()$height
```

    #> [1] 32

``` r
tmp$drop_nulls()$collect()$height
```

    #> [1] 28

``` r
tmp$drop_nulls("mpg")$collect()$height
```

    #> [1] 29

``` r
tmp$drop_nulls(c("mpg", "hp"))$collect()$height
```

    #> [1] 28
