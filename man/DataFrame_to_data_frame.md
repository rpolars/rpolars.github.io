

# Return Polars DataFrame as R data.frame

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L892)

## Description

Return Polars DataFrame as R data.frame

## Usage

<pre><code class='language-R'>DataFrame_to_data_frame(
  ...,
  int64_conversion = polars_options()\$int64_conversion
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_to_data_frame_:_...">…</code>
</td>
<td>
Any args pased to <code>as.data.frame()</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_to_data_frame_:_int64_conversion">int64_conversion</code>
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

An R data.frame

## Examples

``` r
library(polars)

df = pl$DataFrame(iris[1:3, ])
df$to_data_frame()
```

    #>   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
    #> 1          5.1         3.5          1.4         0.2  setosa
    #> 2          4.9         3.0          1.4         0.2  setosa
    #> 3          4.7         3.2          1.3         0.2  setosa
