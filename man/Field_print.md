
# S3 method to print a Field

## Description

S3 method to print a Field

## Usage

<pre><code class='language-R'>## S3 method for class 'RPolarsRField'
print(x, ...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="print.RPolarsRField_:_x">x</code>
</td>
<td>
An object of type <code>“RField”</code>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="print.RPolarsRField_:_...">…</code>
</td>
<td>
Not used.
</td>
</tr>
</table>

## Value

No value returned, it prints in the console.

## Examples

``` r
library(polars)

print(pl$Field("foo", pl$List(pl$UInt64)))
```

    #> Field {
    #>     name: "foo",
    #>     dtype: List(
    #>         UInt64,
    #>     ),
    #> }
