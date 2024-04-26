

# Convert to a character vector

## Description

Convert to a character vector

## Usage

<pre><code class='language-R'>## S3 method for class 'RPolarsSeries'
as.character(x, ..., str_length = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="x">x</code>
</td>
<td>
A Polars Series
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="...">…</code>
</td>
<td>
Not used.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="str_length">str_length</code>
</td>
<td>
An integer. If specified, utf8 or categorical type Series will be
formatted to a string of this length.
</td>
</tr>
</table>

## Examples

``` r
library(polars)

s = as_polars_series(c("foo", "barbaz"))
as.character(s)
```

    #> [1] "foo"    "barbaz"

``` r
as.character(s, str_length = 3)
```

    #> [1] "\"fo…" "\"ba…"
