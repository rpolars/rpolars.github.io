
# append (default immutable)

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/series__series.R#L463)

## Description

append two Series, see details for mutability

## Usage

<pre><code class='language-R'>Series_append(other, immutable = TRUE)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_append_:_other">other</code>
</td>
<td>
Series to append
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_append_:_immutable">immutable</code>
</td>
<td>
bool should append be immutable, default TRUE as mutable operations
should be avoided in plain R API’s.
</td>
</tr>
</table>

## Details

if immutable = FLASE, the Series object will not behave as immutable.
This mean appending to this Series will affect any variable pointing to
this memory location. This will break normal scoping rules of R.
Polars-clones are cheap. Mutable operations are likely never needed in
any sense.

## Value

Series

## Examples

``` r
library(polars)


# default immutable behavior, s_imut and s_imut_copy stay the same
s_imut = pl$Series(1:3)
s_imut_copy = s_imut
s_new = s_imut$append(pl$Series(1:3))
identical(s_imut$to_vector(), s_imut_copy$to_vector())
```

    #> [1] TRUE

``` r
# pypolars-like mutable behavior,s_mut_copy become the same as s_new
s_mut = pl$Series(1:3)
s_mut_copy = s_mut
# must deactivate this to allow to use immutable=FALSE
pl$set_options(strictly_immutable = FALSE)
s_new = s_mut$append(pl$Series(1:3), immutable = FALSE)
identical(s_new$to_vector(), s_mut_copy$to_vector())
```

    #> [1] TRUE
