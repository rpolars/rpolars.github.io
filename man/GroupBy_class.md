
# Operations on Polars grouped DataFrame

## Description

Operations on Polars grouped DataFrame

## Details

The GroupBy class in R, is just another interface on top of the
DataFrame(R wrapper class) in rust polars. Groupby does not use the rust
api for groupby+agg because the groupby-struct is a reference to a
DataFrame and that reference will share lifetime with its parent
DataFrame. There is no way to expose lifetime limited objects via
extendr currently (might be quirky anyhow with R GC). Instead the inputs
for the groupby are just stored on R side, until also agg is called.
Which will end up in a self-owned DataFrame object and all is fine.
groupby aggs are performed via the rust polars LazyGroupBy methods, see
DataFrame.groupby_agg method.

## Value

not applicable
