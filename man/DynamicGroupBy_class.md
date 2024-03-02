

# Operations on Polars DataFrame grouped on time or integer values

## Description

This class comes from <code>\<DataFrame\>$group_by_dynamic()</code>.

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

# get the sum in the following hour relative to the "time" column
df$group_by_dynamic("time", every = "1h")
```

    #> shape: (7, 2)
    #> ┌─────────────────────────┬─────┐
    #> │ time                    ┆ n   │
    #> │ ---                     ┆ --- │
    #> │ datetime[μs, UTC]       ┆ i32 │
    #> ╞═════════════════════════╪═════╡
    #> │ 2021-12-16 00:00:00 UTC ┆ 0   │
    #> │ 2021-12-16 00:30:00 UTC ┆ 1   │
    #> │ 2021-12-16 01:00:00 UTC ┆ 2   │
    #> │ 2021-12-16 01:30:00 UTC ┆ 3   │
    #> │ 2021-12-16 02:00:00 UTC ┆ 4   │
    #> │ 2021-12-16 02:30:00 UTC ┆ 5   │
    #> │ 2021-12-16 03:00:00 UTC ┆ 6   │
    #> └─────────────────────────┴─────┘
