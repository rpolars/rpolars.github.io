
# Drop nulls (missing values)

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/dataframe__frame.R#L374)

## Description

Drop all rows that contain nulls (which correspond to <code>NA</code> in
R).

## Usage

<pre><code class='language-R'>DataFrame_drop_nulls(subset = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_drop_nulls_:_subset">subset</code>
</td>
<td>
A character vector with the names of the column(s) for which nulls are
considered. If <code>NULL</code> (default), use all columns.
</td>
</tr>
</table>

## Value

DataFrame

## Examples

``` r
library(polars)

tmp = mtcars
tmp[1:3, "mpg"] = NA
tmp[4, "hp"] = NA
tmp = pl$DataFrame(tmp)

# number of rows in `tmp` before dropping nulls
tmp$height
```

    #> [1] 32

``` r
tmp$drop_nulls()$height
```

    #> [1] 28

``` r
tmp$drop_nulls("mpg")$height
```

    #> [1] 29

``` r
tmp$drop_nulls(c("mpg", "hp"))$height
```

    #> [1] 28
