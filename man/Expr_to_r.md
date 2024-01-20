
# Convert an Expr to R output

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__expr.R#L3157)

## Description

This is mostly useful to debug an expression. It evaluates the Expr in
an empty DataFrame and return the first Series to R.

## Usage

<pre><code class='language-R'>Expr_to_r(
  df = NULL,
  i = 0,
  ...,
  int64_conversion = pl\$options\$int64_conversion
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_to_r_:_df">df</code>
</td>
<td>
If <code>NULL</code> (default), it evaluates the Expr in an empty
DataFrame. Otherwise, provide a DataFrame that the Expr should be
evaluated in.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_to_r_:_i">i</code>
</td>
<td>
Numeric column to extract. Default is zero (which gives the first
column).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_to_r_:_...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Expr_to_r_:_int64_conversion">int64_conversion</code>
</td>
<td>

How should Int64 values be handled when converting a polars object to R?

<ul>
<li>

<code>“double”</code> (default) converts the integer values to double.

</li>
<li>

<code>“bit64”</code> uses <code>bit64::as.integer64()</code> to do the
conversion (requires the package <code>bit64</code> to be attached).

</li>
<li>

<code>“string”</code> converts Int64 values to character.

</li>
</ul>
</td>
</tr>
</table>

## Value

R object

## Examples

``` r
library(polars)

pl$lit(1:3)$to_r()
```

    #> [1] 1 2 3
