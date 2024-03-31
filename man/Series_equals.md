

# Are two Series equal?

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L921)

## Description

This checks whether two Series are equal in values and in their name.

## Usage

<pre><code class='language-R'>Series_equals(other, null_equal = FALSE, strict = FALSE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_equals_:_other">other</code>
</td>
<td>
Series to compare with.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_equals_:_null_equal">null_equal</code>
</td>
<td>
If <code>TRUE</code>, consider that null values are equal. Overridden by
<code>strict</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_equals_:_strict">strict</code>
</td>
<td>
If <code>TRUE</code>, do not allow similar DataType comparison.
Overrides <code>null_equal</code>.
</td>
</tr>
</table>

## Value

A logical value

## Examples

``` r
library(polars)

as_polars_series(1:4)$equals(as_polars_series(1:4))
```

    #> [1] TRUE

``` r
# names are different
as_polars_series(1:4, "bob")$equals(as_polars_series(1:4))
```

    #> [1] FALSE

``` r
# nulls are different by default
as_polars_series(c(1:4, NA))$equals(as_polars_series(c(1:4, NA)))
```

    #> [1] FALSE

``` r
as_polars_series(c(1:4, NA))$equals(as_polars_series(c(1:4, NA)), null_equal = TRUE)
```

    #> [1] TRUE

``` r
# datatypes are ignored by default
as_polars_series(1:4)$cast(pl$Int16)$equals(as_polars_series(1:4))
```

    #> [1] FALSE

``` r
as_polars_series(1:4)$cast(pl$Int16)$equals(as_polars_series(1:4), strict = TRUE)
```

    #> [1] FALSE
