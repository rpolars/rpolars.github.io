
# print LazyFrame internal method

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/#L)

## Description

can be used i the middle of a method chain

## Usage

<pre><code class='language-R'>LazyFrame_print(x)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_print_:_x">x</code>
</td>
<td>
LazyFrame
</td>
</tr>
</table>

## Format

An object of class <code>character</code> of length 1.

## Value

self

## Examples

``` r
library(polars)

pl$LazyFrame(iris)$print()
```

    #> DF ["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]; PROJECT */5 COLUMNS; SELECTION: "None"

    #> [1] "polars LazyFrame naive plan: (run ldf$describe_optimized_plan() to see the optimized plan)"
    #> DF ["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]; PROJECT */5 COLUMNS; SELECTION: "None"
