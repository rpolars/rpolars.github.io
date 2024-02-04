

# Are Series’s equal?

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/series__series.R#L821)

## Description

Check if series is equal with another Series.

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
Series to compare with
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_equals_:_null_equal">null_equal</code>
</td>
<td>
bool if TRUE, (Null==Null) is true and not Null/NA. Overridden by
strict.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_equals_:_strict">strict</code>
</td>
<td>
bool if TRUE, do not allow similar DataType comparison. Overrides
null_equal.
</td>
</tr>
</table>

## Format

method

## Value

bool

## Examples

``` r
library(polars)

pl$Series(1:4, "bob")$equals(pl$Series(1:4))
```

    #> [1] FALSE
