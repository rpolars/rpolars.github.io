

# Create a Date expression

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/functions__lazy.R#L1183)

## Description

Create a Date expression

## Usage

<pre><code class='language-R'>pl_date(year, month, day)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="year">year</code>
</td>
<td>
An Expr or something coercible to an Expr, that must return an integer.
Strings are parsed as column names. Floats are cast to integers.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="month">month</code>
</td>
<td>
An Expr or something coercible to an Expr, that must return an integer
between 1 and 12. Strings are parsed as column names. Floats are cast to
integers.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="day">day</code>
</td>
<td>
An Expr or something coercible to an Expr, that must return an integer
between 1 and 31. Strings are parsed as column names. Floats are cast to
integers.
</td>
</tr>
</table>

## Value

An Expr of type Date

## See Also

<ul>
<li>

<code>pl$datetime()</code>

</li>
<li>

<code>pl$time()</code>

</li>
</ul>

## Examples

``` r
library(polars)

df = pl$DataFrame(year = 2019:2021, month = 9:11, day = 10:12)

df$with_columns(
  date_from_cols = pl$date("year", "month", "day"),
  date_from_lit = pl$date(2020, 3, 5),
  date_from_mix = pl$date("year", 3, 5)
)
```

    #> shape: (3, 6)
    #> ┌──────┬───────┬─────┬────────────────┬───────────────┬───────────────┐
    #> │ year ┆ month ┆ day ┆ date_from_cols ┆ date_from_lit ┆ date_from_mix │
    #> │ ---  ┆ ---   ┆ --- ┆ ---            ┆ ---           ┆ ---           │
    #> │ i32  ┆ i32   ┆ i32 ┆ date           ┆ date          ┆ date          │
    #> ╞══════╪═══════╪═════╪════════════════╪═══════════════╪═══════════════╡
    #> │ 2019 ┆ 9     ┆ 10  ┆ 2019-09-10     ┆ 2020-03-05    ┆ 2019-03-05    │
    #> │ 2020 ┆ 10    ┆ 11  ┆ 2020-10-11     ┆ 2020-03-05    ┆ 2020-03-05    │
    #> │ 2021 ┆ 11    ┆ 12  ┆ 2021-11-12     ┆ 2020-03-05    ┆ 2021-03-05    │
    #> └──────┴───────┴─────┴────────────────┴───────────────┴───────────────┘

``` r
# floats are coerced to integers
df$with_columns(
  date_floats = pl$date(2018.8, 5.3, 1)
)
```

    #> shape: (3, 4)
    #> ┌──────┬───────┬─────┬─────────────┐
    #> │ year ┆ month ┆ day ┆ date_floats │
    #> │ ---  ┆ ---   ┆ --- ┆ ---         │
    #> │ i32  ┆ i32   ┆ i32 ┆ date        │
    #> ╞══════╪═══════╪═════╪═════════════╡
    #> │ 2019 ┆ 9     ┆ 10  ┆ 2018-05-01  │
    #> │ 2020 ┆ 10    ┆ 11  ┆ 2018-05-01  │
    #> │ 2021 ┆ 11    ┆ 12  ┆ 2018-05-01  │
    #> └──────┴───────┴─────┴─────────────┘

``` r
# if date can't be constructed, it returns null
df$with_columns(
  date_floats = pl$date(pl$lit("abc"), -2, 1)
)
```

    #> shape: (3, 4)
    #> ┌──────┬───────┬─────┬─────────────┐
    #> │ year ┆ month ┆ day ┆ date_floats │
    #> │ ---  ┆ ---   ┆ --- ┆ ---         │
    #> │ i32  ┆ i32   ┆ i32 ┆ date        │
    #> ╞══════╪═══════╪═════╪═════════════╡
    #> │ 2019 ┆ 9     ┆ 10  ┆ null        │
    #> │ 2020 ┆ 10    ┆ 11  ┆ null        │
    #> │ 2021 ┆ 11    ┆ 12  ┆ null        │
    #> └──────┴───────┴─────┴─────────────┘
