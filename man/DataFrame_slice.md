
# Slice

[**Source code**](https://github.com/pola-rs/r-polars/tree/3908b5beab9ec917b825bad8f9a820caad37cb4a/R/dataframe__frame.R#L1224)

## Description

Get a slice of the DataFrame.

## Usage

<pre><code class='language-R'>DataFrame_slice(offset, length = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_slice_:_offset">offset</code>
</td>
<td>
Start index, can be a negative value. This is 0-indexed, so <code>offset
= 1</code> doesn’t include the first row.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_slice_:_length">length</code>
</td>
<td>
Length of the slice. If <code>NULL</code> (default), all rows starting
at the offset will be selected.
</td>
</tr>
</table>

## Value

DataFrame

## Examples

``` r
library(polars)

# skip the first 2 rows and take the 4 following rows
pl$DataFrame(mtcars)$slice(2, 4)
```

    #> shape: (4, 11)
    #> ┌──────┬─────┬───────┬───────┬───┬─────┬─────┬──────┬──────┐
    #> │ mpg  ┆ cyl ┆ disp  ┆ hp    ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
    #> │ ---  ┆ --- ┆ ---   ┆ ---   ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
    #> │ f64  ┆ f64 ┆ f64   ┆ f64   ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
    #> ╞══════╪═════╪═══════╪═══════╪═══╪═════╪═════╪══════╪══════╡
    #> │ 22.8 ┆ 4.0 ┆ 108.0 ┆ 93.0  ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 1.0  │
    #> │ 21.4 ┆ 6.0 ┆ 258.0 ┆ 110.0 ┆ … ┆ 1.0 ┆ 0.0 ┆ 3.0  ┆ 1.0  │
    #> │ 18.7 ┆ 8.0 ┆ 360.0 ┆ 175.0 ┆ … ┆ 0.0 ┆ 0.0 ┆ 3.0  ┆ 2.0  │
    #> │ 18.1 ┆ 6.0 ┆ 225.0 ┆ 105.0 ┆ … ┆ 1.0 ┆ 0.0 ┆ 3.0  ┆ 1.0  │
    #> └──────┴─────┴───────┴───────┴───┴─────┴─────┴──────┴──────┘

``` r
# this is equivalent to:
mtcars[3:6, ]
```

    #>                    mpg cyl disp  hp drat    wt  qsec vs am gear carb
    #> Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
    #> Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
    #> Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
    #> Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1
