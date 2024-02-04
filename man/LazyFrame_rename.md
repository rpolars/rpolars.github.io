

# Rename columns of a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/lazyframe__lazy.R#L1357)

## Description

Rename columns of a DataFrame

## Usage

<pre><code class='language-R'>LazyFrame_rename(...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="LazyFrame_rename_:_...">…</code>
</td>
<td>

One of the following:

<ul>
<li>

params like <code>new_name = “old_name”</code> to rename selected
variables.

</li>
<li>

as above but with params wrapped in a list

</li>
</ul>
</td>
</tr>
</table>

## Value

LazyFrame

## Examples

``` r
library(polars)

pl$LazyFrame(mtcars)$
  rename(miles_per_gallon = "mpg", horsepower = "hp")$
  collect()
```

    #> shape: (32, 11)
    #> ┌──────────────────┬─────┬───────┬────────────┬───┬─────┬─────┬──────┬──────┐
    #> │ miles_per_gallon ┆ cyl ┆ disp  ┆ horsepower ┆ … ┆ vs  ┆ am  ┆ gear ┆ carb │
    #> │ ---              ┆ --- ┆ ---   ┆ ---        ┆   ┆ --- ┆ --- ┆ ---  ┆ ---  │
    #> │ f64              ┆ f64 ┆ f64   ┆ f64        ┆   ┆ f64 ┆ f64 ┆ f64  ┆ f64  │
    #> ╞══════════════════╪═════╪═══════╪════════════╪═══╪═════╪═════╪══════╪══════╡
    #> │ 21.0             ┆ 6.0 ┆ 160.0 ┆ 110.0      ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
    #> │ 21.0             ┆ 6.0 ┆ 160.0 ┆ 110.0      ┆ … ┆ 0.0 ┆ 1.0 ┆ 4.0  ┆ 4.0  │
    #> │ 22.8             ┆ 4.0 ┆ 108.0 ┆ 93.0       ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 1.0  │
    #> │ 21.4             ┆ 6.0 ┆ 258.0 ┆ 110.0      ┆ … ┆ 1.0 ┆ 0.0 ┆ 3.0  ┆ 1.0  │
    #> │ …                ┆ …   ┆ …     ┆ …          ┆ … ┆ …   ┆ …   ┆ …    ┆ …    │
    #> │ 15.8             ┆ 8.0 ┆ 351.0 ┆ 264.0      ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 4.0  │
    #> │ 19.7             ┆ 6.0 ┆ 145.0 ┆ 175.0      ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 6.0  │
    #> │ 15.0             ┆ 8.0 ┆ 301.0 ┆ 335.0      ┆ … ┆ 0.0 ┆ 1.0 ┆ 5.0  ┆ 8.0  │
    #> │ 21.4             ┆ 4.0 ┆ 121.0 ┆ 109.0      ┆ … ┆ 1.0 ┆ 1.0 ┆ 4.0  ┆ 2.0  │
    #> └──────────────────┴─────┴───────┴────────────┴───┴─────┴─────┴──────┴──────┘
