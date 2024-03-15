

# Change name of Series

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/after-wrappers.R#L20)

## Description

Change name of Series

## Usage

<pre><code class='language-R'>Series_alias(name)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_alias_:_name">name</code>
</td>
<td>
New name.
</td>
</tr>
</table>

## Value

Series

## Examples

``` r
library(polars)

pl$Series(1:3, name = "alice")$alias("bob")
```

    #> polars Series: shape: (3,)
    #> Series: 'bob' [i32]
    #> [
    #>  1
    #>  2
    #>  3
    #> ]
