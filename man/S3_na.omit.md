

# Drop missing values

## Description

Drop missing values

## Usage

<pre><code class='language-R'>## S3 method for class 'RPolarsLazyFrame'
na.omit(object, subset = NULL, ...)

# S3 method for class 'RPolarsDataFrame'
na.omit(object, subset = NULL, ...)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="na.omit.RPolarsLazyFrame_:_object">object</code>
</td>
<td>
A DataFrame or LazyFrame
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="na.omit.RPolarsLazyFrame_:_subset">subset</code>
</td>
<td>
Character vector of column names to drop missing values from.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="na.omit.RPolarsLazyFrame_:_...">…</code>
</td>
<td>
Not used.
</td>
</tr>
</table>

## Examples

``` r
library(polars)

df = pl$DataFrame(data.frame(a = c(NA, 2:10), b = c(1, NA, 3:10)))$lazy()
na.omit(df)
```

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #> FILTER col("a").is_not_null().all_horizontal([col("b").is_not_null()]) FROM
    #> DF ["a", "b"]; PROJECT */2 COLUMNS; SELECTION: "None"

``` r
na.omit(df, subset = "a")
```

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #> FILTER col("a").is_not_null().all_horizontal() FROM
    #> DF ["a", "b"]; PROJECT */2 COLUMNS; SELECTION: "None"

``` r
na.omit(df, subset = c("a", "b"))
```

    #> polars LazyFrame
    #>  $describe_optimized_plan() : Show the optimized query plan.
    #> 
    #> Naive plan:
    #> FILTER [(col("a").is_not_null()) & (col("b").is_not_null())] FROM
    #> DF ["a", "b"]; PROJECT */2 COLUMNS; SELECTION: "None"
