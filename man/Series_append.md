

# Append two Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L614)

## Description

Append two Series

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
Series to append.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_append_:_immutable">immutable</code>
</td>
<td>
Should the <code>other</code> Series be immutable? Default is
<code>TRUE</code>.
</td>
</tr>
</table>

## Details

If <code>immutable = FALSE</code>, the Series object will not behave as
immutable. This means that appending to this Series will affect any
variable pointing to this memory location. This will break normal
scoping rules of R. Setting <code>immutable = FALSE</code> is
discouraged as it can have undesirable side effects and cloning Polars
Series is a cheap operation.

## Value

Series

## Examples

``` r
library(polars)


# default immutable behavior, s_imut and s_imut_copy stay the same
s_imut = pl$Series(1:3)
s_imut_copy = s_imut
s_new = s_imut$append(pl$Series(1:3))
s_new
```

    #> polars Series: shape: (6,)
    #> Series: '' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #>  1
    #>  2
    #>  3
    #> ]

``` r
# the original Series didn't change
s_imut
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #> ]

``` r
s_imut_copy
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #> ]

``` r
# enabling mutable behavior requires setting a global option
withr::with_options(
  list(polars.strictly_immutable = FALSE),
  {
    s_mut = pl$Series(1:3)
    s_mut_copy = s_mut
    s_new = s_mut$append(pl$Series(1:3), immutable = FALSE)
    print(s_new)

    # the original Series also changed since it's mutable
    print(s_mut)
    print(s_mut_copy)
  }
)
```

    #> polars Series: shape: (6,)
    #> Series: '' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #>  1
    #>  2
    #>  3
    #> ]
    #> polars Series: shape: (6,)
    #> Series: '' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #>  1
    #>  2
    #>  3
    #> ]
    #> polars Series: shape: (6,)
    #> Series: '' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #>  1
    #>  2
    #>  3
    #> ]
