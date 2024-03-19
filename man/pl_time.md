

# Create a Time expression

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L1197)

## Description

Create a Time expression

## Usage

<pre><code class='language-R'>pl_time(hour = NULL, minute = NULL, second = NULL, microsecond = NULL)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_time_:_hour">hour</code>
</td>
<td>
An Expr or something coercible to an Expr, that must return an integer
between 0 and 23. Strings are parsed as column names. Floats are cast to
integers.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_time_:_minute">minute</code>
</td>
<td>
An Expr or something coercible to an Expr, that must return an integer
between 0 and 59. Strings are parsed as column names. Floats are cast to
integers.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_time_:_second">second</code>
</td>
<td>
An Expr or something coercible to an Expr, that must return an integer
between 0 and 59. Strings are parsed as column names. Floats are cast to
integers.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_time_:_microsecond">microsecond</code>
</td>
<td>
An Expr or something coercible to an Expr, that must return an integer
between 0 and 999,999. Strings are parsed as column names. Floats are
cast to integers.
</td>
</tr>
</table>

## Value

An Expr of type Time

## See Also

<ul>
<li>

<code>pl$datetime()</code>

</li>
<li>

<code>pl$date()</code>

</li>
</ul>

## Examples

``` r
library(polars)

df = pl$DataFrame(hour = 19:21, min = 9:11, sec = 10:12, micro = 1)

df$with_columns(
  time_from_cols = pl$time("hour", "min", "sec", "micro"),
  time_from_lit = pl$time(12, 3, 5),
  time_from_mix = pl$time("hour", 3, 5)
)
```

    #> shape: (3, 7)
    #> ┌──────┬─────┬─────┬───────┬─────────────────┬───────────────┬───────────────┐
    #> │ hour ┆ min ┆ sec ┆ micro ┆ time_from_cols  ┆ time_from_lit ┆ time_from_mix │
    #> │ ---  ┆ --- ┆ --- ┆ ---   ┆ ---             ┆ ---           ┆ ---           │
    #> │ i32  ┆ i32 ┆ i32 ┆ f64   ┆ time            ┆ time          ┆ time          │
    #> ╞══════╪═════╪═════╪═══════╪═════════════════╪═══════════════╪═══════════════╡
    #> │ 19   ┆ 9   ┆ 10  ┆ 1.0   ┆ 19:09:10.000001 ┆ 12:03:05      ┆ 19:03:05      │
    #> │ 20   ┆ 10  ┆ 11  ┆ 1.0   ┆ 20:10:11.000001 ┆ 12:03:05      ┆ 20:03:05      │
    #> │ 21   ┆ 11  ┆ 12  ┆ 1.0   ┆ 21:11:12.000001 ┆ 12:03:05      ┆ 21:03:05      │
    #> └──────┴─────┴─────┴───────┴─────────────────┴───────────────┴───────────────┘

``` r
# floats are coerced to integers
df$with_columns(
  time_floats = pl$time(12.5, 5.3, 1)
)
```

    #> shape: (3, 5)
    #> ┌──────┬─────┬─────┬───────┬─────────────┐
    #> │ hour ┆ min ┆ sec ┆ micro ┆ time_floats │
    #> │ ---  ┆ --- ┆ --- ┆ ---   ┆ ---         │
    #> │ i32  ┆ i32 ┆ i32 ┆ f64   ┆ time        │
    #> ╞══════╪═════╪═════╪═══════╪═════════════╡
    #> │ 19   ┆ 9   ┆ 10  ┆ 1.0   ┆ 12:05:01    │
    #> │ 20   ┆ 10  ┆ 11  ┆ 1.0   ┆ 12:05:01    │
    #> │ 21   ┆ 11  ┆ 12  ┆ 1.0   ┆ 12:05:01    │
    #> └──────┴─────┴─────┴───────┴─────────────┘

``` r
# if time can't be constructed, it returns null
df$with_columns(
  time_floats = pl$time(pl$lit("abc"), -2, 1)
)
```

    #> shape: (3, 5)
    #> ┌──────┬─────┬─────┬───────┬─────────────┐
    #> │ hour ┆ min ┆ sec ┆ micro ┆ time_floats │
    #> │ ---  ┆ --- ┆ --- ┆ ---   ┆ ---         │
    #> │ i32  ┆ i32 ┆ i32 ┆ f64   ┆ time        │
    #> ╞══════╪═════╪═════╪═══════╪═════════════╡
    #> │ 19   ┆ 9   ┆ 10  ┆ 1.0   ┆ null        │
    #> │ 20   ┆ 10  ┆ 11  ┆ 1.0   ┆ null        │
    #> │ 21   ┆ 11  ┆ 12  ┆ 1.0   ┆ null        │
    #> └──────┴─────┴─────┴───────┴─────────────┘
