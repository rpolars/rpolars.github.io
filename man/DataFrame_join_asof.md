

# Perform joins on nearest keys

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/dataframe__frame.R#L1309)

## Description

This is similar to a left-join except that we match on nearest key
rather than equal keys.

## Usage

<pre><code class='language-R'>DataFrame_join_asof(
  other,
  ...,
  left_on = NULL,
  right_on = NULL,
  on = NULL,
  by_left = NULL,
  by_right = NULL,
  by = NULL,
  strategy = c("backward", "forward", "nearest"),
  suffix = "_right",
  tolerance = NULL,
  allow_parallel = TRUE,
  force_parallel = FALSE
)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_join_asof_:_other">other</code>
</td>
<td>
DataFrame or LazyFrame
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_join_asof_:_...">…</code>
</td>
<td>
Not used, blocks use of further positional arguments
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_join_asof_:_left_on">left_on</code>,
<code id="DataFrame_join_asof_:_right_on">right_on</code>
</td>
<td>
Same as <code>on</code> but only for the left or the right DataFrame.
They must have the same length.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_join_asof_:_on">on</code>
</td>
<td>
Either a vector of column names or a list of expressions and/or strings.
Use <code>left_on</code> and <code>right_on</code> if the column names
to match on are different between the two DataFrames.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_join_asof_:_by_left">by_left</code>,
<code id="DataFrame_join_asof_:_by_right">by_right</code>
</td>
<td>
Same as <code>by</code> but only for the left or the right table. They
must have the same length.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_join_asof_:_by">by</code>
</td>
<td>
Join on these columns before performing asof join. Either a vector of
column names or a list of expressions and/or strings. Use
<code>left_by</code> and <code>right_by</code> if the column names to
match on are different between the two tables.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_join_asof_:_strategy">strategy</code>
</td>
<td>

Strategy for where to find match:

<ul>
<li>

"backward" (default): search for the last row in the right table whose
<code>on</code> key is less than or equal to the left key.

</li>
<li>

"forward": search for the first row in the right table whose
<code>on</code> key is greater than or equal to the left key.

</li>
<li>

"nearest": search for the last row in the right table whose value is
nearest to the left key. String keys are not currently supported for a
nearest search.

</li>
</ul>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_join_asof_:_suffix">suffix</code>
</td>
<td>
Suffix to add to duplicated column names.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_join_asof_:_tolerance">tolerance</code>
</td>
<td>

Numeric tolerance. By setting this the join will only be done if the
near keys are within this distance. If an asof join is done on columns
of dtype "Date", "Datetime", "Duration" or "Time" you can use the
following values:

<pre>- 1ns   (1 nanosecond)
- 1us   (1 microsecond)
- 1ms   (1 millisecond)
- 1s    (1 second)
- 1m    (1 minute)
- 1h    (1 hour)
- 1d    (1 day)
- 1w    (1 week)
- 1mo   (1 calendar month) // currently not available, as interval is not fixed
- 1y    (1 calendar year)  // currently not available, as interval is not fixed
- 1i    (1 index count)
</pre>

Or combine them: "3d12h4m25s" \# 3 days, 12 hours, 4 minutes, and 25
seconds

There may be a circumstance where R types are not sufficient to express
a numeric tolerance. In that case, you can use the expression syntax
like <code>tolerance = pl$lit(42)$cast(pl$Uint64)</code>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_join_asof_:_allow_parallel">allow_parallel</code>
</td>
<td>
Allow the physical plan to optionally evaluate the computation of both
DataFrames up to the join in parallel.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_join_asof_:_force_parallel">force_parallel</code>
</td>
<td>
Force the physical plan to evaluate the computation of both DataFrames
up to the join in parallel.
</td>
</tr>
</table>

## Details

Both tables (DataFrames or LazyFrames) must be sorted by the asof_join
key.

## Value

New joined DataFrame

## Examples

``` r
library(polars)

# create two DataFrames to join asof
gdp = pl$DataFrame(
  date = as.Date(c("2015-1-1", "2016-1-1", "2017-5-1", "2018-1-1", "2019-1-1")),
  gdp = c(4321, 4164, 4411, 4566, 4696),
  group = c("b", "a", "a", "b", "b")
)

pop = pl$DataFrame(
  date = as.Date(c("2016-5-12", "2017-5-12", "2018-5-12", "2019-5-12")),
  population = c(82.19, 82.66, 83.12, 83.52),
  group = c("b", "b", "a", "a")
)

# optional make sure tables are already sorted with "on" join-key
gdp = gdp$sort("date")
pop = pop$sort("date")

# Left-join_asof DataFrame pop with gdp on "date"
# Look backward in gdp to find closest matching date
pop$join_asof(gdp, on = "date", strategy = "backward")
```

    #> shape: (4, 5)
    #> ┌────────────┬────────────┬───────┬────────┬─────────────┐
    #> │ date       ┆ population ┆ group ┆ gdp    ┆ group_right │
    #> │ ---        ┆ ---        ┆ ---   ┆ ---    ┆ ---         │
    #> │ date       ┆ f64        ┆ str   ┆ f64    ┆ str         │
    #> ╞════════════╪════════════╪═══════╪════════╪═════════════╡
    #> │ 2016-05-12 ┆ 82.19      ┆ b     ┆ 4164.0 ┆ a           │
    #> │ 2017-05-12 ┆ 82.66      ┆ b     ┆ 4411.0 ┆ a           │
    #> │ 2018-05-12 ┆ 83.12      ┆ a     ┆ 4566.0 ┆ b           │
    #> │ 2019-05-12 ┆ 83.52      ┆ a     ┆ 4696.0 ┆ b           │
    #> └────────────┴────────────┴───────┴────────┴─────────────┘

``` r
# .... and forward
pop$join_asof(gdp, on = "date", strategy = "forward")
```

    #> shape: (4, 5)
    #> ┌────────────┬────────────┬───────┬────────┬─────────────┐
    #> │ date       ┆ population ┆ group ┆ gdp    ┆ group_right │
    #> │ ---        ┆ ---        ┆ ---   ┆ ---    ┆ ---         │
    #> │ date       ┆ f64        ┆ str   ┆ f64    ┆ str         │
    #> ╞════════════╪════════════╪═══════╪════════╪═════════════╡
    #> │ 2016-05-12 ┆ 82.19      ┆ b     ┆ 4411.0 ┆ a           │
    #> │ 2017-05-12 ┆ 82.66      ┆ b     ┆ 4566.0 ┆ b           │
    #> │ 2018-05-12 ┆ 83.12      ┆ a     ┆ 4696.0 ┆ b           │
    #> │ 2019-05-12 ┆ 83.52      ┆ a     ┆ null   ┆ null        │
    #> └────────────┴────────────┴───────┴────────┴─────────────┘

``` r
# join by a group: "only look within within group"
pop$join_asof(gdp, on = "date", by = "group", strategy = "backward")
```

    #> shape: (4, 4)
    #> ┌────────────┬────────────┬───────┬────────┐
    #> │ date       ┆ population ┆ group ┆ gdp    │
    #> │ ---        ┆ ---        ┆ ---   ┆ ---    │
    #> │ date       ┆ f64        ┆ str   ┆ f64    │
    #> ╞════════════╪════════════╪═══════╪════════╡
    #> │ 2016-05-12 ┆ 82.19      ┆ b     ┆ 4321.0 │
    #> │ 2017-05-12 ┆ 82.66      ┆ b     ┆ 4321.0 │
    #> │ 2018-05-12 ┆ 83.12      ┆ a     ┆ 4411.0 │
    #> │ 2019-05-12 ┆ 83.52      ┆ a     ┆ 4411.0 │
    #> └────────────┴────────────┴───────┴────────┘

``` r
# only look 2 weeks and 2 days back
pop$join_asof(gdp, on = "date", strategy = "backward", tolerance = "2w2d")
```

    #> shape: (4, 5)
    #> ┌────────────┬────────────┬───────┬────────┬─────────────┐
    #> │ date       ┆ population ┆ group ┆ gdp    ┆ group_right │
    #> │ ---        ┆ ---        ┆ ---   ┆ ---    ┆ ---         │
    #> │ date       ┆ f64        ┆ str   ┆ f64    ┆ str         │
    #> ╞════════════╪════════════╪═══════╪════════╪═════════════╡
    #> │ 2016-05-12 ┆ 82.19      ┆ b     ┆ null   ┆ null        │
    #> │ 2017-05-12 ┆ 82.66      ┆ b     ┆ 4411.0 ┆ a           │
    #> │ 2018-05-12 ┆ 83.12      ┆ a     ┆ null   ┆ null        │
    #> │ 2019-05-12 ┆ 83.52      ┆ a     ┆ null   ┆ null        │
    #> └────────────┴────────────┴───────┴────────┴─────────────┘

``` r
# only look 11 days back (numeric tolerance depends on polars type, <date> is in days)
pop$join_asof(gdp, on = "date", strategy = "backward", tolerance = 11)
```

    #> shape: (4, 5)
    #> ┌────────────┬────────────┬───────┬────────┬─────────────┐
    #> │ date       ┆ population ┆ group ┆ gdp    ┆ group_right │
    #> │ ---        ┆ ---        ┆ ---   ┆ ---    ┆ ---         │
    #> │ date       ┆ f64        ┆ str   ┆ f64    ┆ str         │
    #> ╞════════════╪════════════╪═══════╪════════╪═════════════╡
    #> │ 2016-05-12 ┆ 82.19      ┆ b     ┆ null   ┆ null        │
    #> │ 2017-05-12 ┆ 82.66      ┆ b     ┆ 4411.0 ┆ a           │
    #> │ 2018-05-12 ┆ 83.12      ┆ a     ┆ null   ┆ null        │
    #> │ 2019-05-12 ┆ 83.52      ┆ a     ┆ null   ┆ null        │
    #> └────────────┴────────────┴───────┴────────┴─────────────┘
