

# Fills the string with zeroes.

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/expr__string.R#L382)

## Description

Add zeroes to a string until it reaches <code>n</code> characters. If
the number of characters is already greater than <code>n</code>, the
string is not modified.

## Usage

<pre><code class='language-R'>ExprStr_zfill(alignment)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="ExprStr_zfill_:_alignment">alignment</code>
</td>
<td>
Fill the value up to this length.
</td>
</tr>
</table>

## Details

Return a copy of the string left filled with ASCII ‘0’ digits to make a
string of length width.

A leading sign prefix (‘+’/‘-’) is handled by inserting the padding
after the sign character rather than before. The original string is
returned if width is less than or equal to <code>len(s)</code>.

## Value

Expr

## Examples

``` r
library(polars)

some_floats_expr = pl$lit(c(0, 10, -5, 5))

# cast to String and ljust alignment = 5, and view as R char vector
some_floats_expr$cast(pl$String)$str$zfill(5)$to_r()
```

    #> [1] "000.0" "010.0" "-05.0" "005.0"

``` r
# cast to int and the to utf8 and then ljust alignment = 5, and view as R
# char vector
some_floats_expr$cast(pl$Int64)$cast(pl$String)$str$zfill(5)$to_r()
```

    #> [1] "00000" "00010" "-0005" "00005"
