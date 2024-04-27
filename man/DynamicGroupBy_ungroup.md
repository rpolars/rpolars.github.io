

# Ungroup a DynamicGroupBy object

[**Source code**](https://github.com/pola-rs/r-polars/tree/8dac37e8bf89bcd080a13d0ed20dd1dc2bee615f/R/group_by_dynamic.R#L124)

## Description

Revert the <code style="white-space: pre;">$group_by_dynamic()</code>
operation. Doing
<code style="white-space: pre;">\<DataFrame\>$group_by_dynamic(…)$ungroup()</code>
returns the original <code>DataFrame</code>.

## Usage

<pre><code class='language-R'>DynamicGroupBy_ungroup()
</code></pre>

## Value

DataFrame

## Examples

``` r
library(polars)

df = pl$DataFrame(
  time = pl$date_range(
    start = strptime("2021-12-16 00:00:00", format = "%Y-%m-%d %H:%M:%S", tz = "UTC"),
    end = strptime("2021-12-16 03:00:00", format = "%Y-%m-%d %H:%M:%S", tz = "UTC"),
    interval = "30m"
  ),
  n = 0:6
)
df
```

    #> shape: (7, 2)
    #> ┌─────────────────────────┬─────┐
    #> │ time                    ┆ n   │
    #> │ ---                     ┆ --- │
    #> │ datetime[ms, UTC]       ┆ i32 │
    #> ╞═════════════════════════╪═════╡
    #> │ 2021-12-16 00:00:00 UTC ┆ 0   │
    #> │ 2021-12-16 00:30:00 UTC ┆ 1   │
    #> │ 2021-12-16 01:00:00 UTC ┆ 2   │
    #> │ 2021-12-16 01:30:00 UTC ┆ 3   │
    #> │ 2021-12-16 02:00:00 UTC ┆ 4   │
    #> │ 2021-12-16 02:30:00 UTC ┆ 5   │
    #> │ 2021-12-16 03:00:00 UTC ┆ 6   │
    #> └─────────────────────────┴─────┘

``` r
df$group_by_dynamic("time", every = "1h")$ungroup()
```

    #> shape: (7, 2)
    #> ┌─────────────────────────┬─────┐
    #> │ time                    ┆ n   │
    #> │ ---                     ┆ --- │
    #> │ datetime[ms, UTC]       ┆ i32 │
    #> ╞═════════════════════════╪═════╡
    #> │ 2021-12-16 00:00:00 UTC ┆ 0   │
    #> │ 2021-12-16 00:30:00 UTC ┆ 1   │
    #> │ 2021-12-16 01:00:00 UTC ┆ 2   │
    #> │ 2021-12-16 01:30:00 UTC ┆ 3   │
    #> │ 2021-12-16 02:00:00 UTC ┆ 4   │
    #> │ 2021-12-16 02:30:00 UTC ┆ 5   │
    #> │ 2021-12-16 03:00:00 UTC ┆ 6   │
    #> └─────────────────────────┴─────┘
