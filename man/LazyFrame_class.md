

# Inner workings of the LazyFrame-class

## Description

The <code>LazyFrame</code>-class is simply two environments of
respectively the public and private methods/function calls to the polars
rust side. The instantiated <code>LazyFrame</code>-object is an
<code>externalptr</code> to a lowlevel rust polars LazyFrame object. The
pointer address is the only statefullness of the LazyFrame object on the
R side. Any other state resides on the rust side. The S3 method
<code>.DollarNames.RPolarsLazyFrame</code> exposes all public
<code style="white-space: pre;">$foobar()</code>-methods which are
callable onto the object.

Most methods return another <code>LazyFrame</code>-class instance or
similar which allows for method chaining. This class system in lack of a
better name could be called "environment classes" and is the same class
system extendr provides, except here there is both a public and private
set of methods. For implementation reasons, the private methods are
external and must be called from
<code>.pr$LazyFrame$methodname()</code>. Also, all private methods must
take any self as an argument, thus they are pure functions. Having the
private methods as pure functions solved/simplified self-referential
complications.

<code>DataFrame</code> and <code>LazyFrame</code> can both be said to be
a <code>Frame</code>. To convert use <code>\<DataFrame\>$lazy()</code>
and <code>\<LazyFrame\>$collect()</code>. You can also create a
<code>LazyFrame</code> directly with <code>pl$LazyFrame()</code>. This
is quite similar to the lazy-collect syntax of the <code>dplyr</code>
package to interact with database connections such as SQL variants. Most
SQL databases would be able to perform the same optimizations as polars
such predicate pushdown and projection pushdown. However polars can
interact and optimize queries with both SQL DBs and other data sources
such parquet files simultaneously.

## Active bindings

<h4>
columns
</h4>

<code style="white-space: pre;">$columns</code> returns a character
vector with the column names.

<h4>
dtypes
</h4>

<code style="white-space: pre;">$dtypes</code> returns a unnamed list
with the data type of each column.

<h4>
schema
</h4>

<code style="white-space: pre;">$schema</code> returns a named list with
the data type of each column.

<h4>
width
</h4>

<code style="white-space: pre;">$width</code> returns the number of
columns in the LazyFrame.

## Conversion to R data types considerations

When converting Polars objects, such as DataFrames to R objects, for
example via the <code>as.data.frame()</code> generic function, each type
in the Polars object is converted to an R type. In some cases, an error
may occur because the conversion is not appropriate. In particular,
there is a high possibility of an error when converting a Datetime type
without a time zone. A Datetime type without a time zone in Polars is
converted to the POSIXct type in R, which takes into account the time
zone in which the R session is running (which can be checked with the
<code>Sys.timezone()</code> function). In this case, if ambiguous times
are included, a conversion error will occur. In such cases, change the
session time zone using <code>Sys.setenv(TZ = "UTC")</code> and then
perform the conversion, or use the <code>$dt$replace_time_zone()</code>
method on the Datetime type column to explicitly specify the time zone
before conversion.

<pre># Due to daylight savings, clocks were turned forward 1 hour on Sunday, March 8, 2020, 2:00:00 am
# so this particular date-time doesn't exist
non_existent_time = as_polars_series("2020-03-08 02:00:00")\$str\$strptime(pl\$Datetime(), "%F %T")

withr::with_envvar(
  new = c(TZ = "America/New_York"),
  {
    tryCatch(
      # This causes an error due to the time zone (the `TZ` env var is affected).
      as.vector(non_existent_time),
      error = function(e) e
    )
  }
)
#&gt; &lt;error: in to_r: ComputeError(ErrString("datetime '2020-03-08 02:00:00' is non-existent in time zone 'America/New_York'. You may be able to use `non_existent='null'` to return `null` in this case.")) When calling: devtools::document()&gt;

withr::with_envvar(
  new = c(TZ = "America/New_York"),
  {
    # This is safe.
    as.vector(non_existent_time\$dt\$replace_time_zone("UTC"))
  }
)
#&gt; [1] "2020-03-08 02:00:00 UTC"
</pre>

## Examples

``` r
library(polars)

# see all exported methods
ls(.pr$env$RPolarsLazyFrame)
```

    #>  [1] "clear"                   "clone"                  
    #>  [3] "collect"                 "collect_in_background"  
    #>  [5] "columns"                 "describe_optimized_plan"
    #>  [7] "describe_plan"           "drop"                   
    #>  [9] "drop_nulls"              "dtypes"                 
    #> [11] "explode"                 "fetch"                  
    #> [13] "fill_nan"                "fill_null"              
    #> [15] "filter"                  "first"                  
    #> [17] "get_optimization_toggle" "group_by"               
    #> [19] "group_by_dynamic"        "head"                   
    #> [21] "join"                    "join_asof"              
    #> [23] "last"                    "limit"                  
    #> [25] "max"                     "mean"                   
    #> [27] "median"                  "melt"                   
    #> [29] "min"                     "print"                  
    #> [31] "profile"                 "quantile"               
    #> [33] "rename"                  "reverse"                
    #> [35] "rolling"                 "schema"                 
    #> [37] "select"                  "select_seq"             
    #> [39] "set_optimization_toggle" "shift"                  
    #> [41] "shift_and_fill"          "sink_csv"               
    #> [43] "sink_ipc"                "sink_ndjson"            
    #> [45] "sink_parquet"            "slice"                  
    #> [47] "sort"                    "std"                    
    #> [49] "sum"                     "tail"                   
    #> [51] "to_dot"                  "unique"                 
    #> [53] "unnest"                  "var"                    
    #> [55] "width"                   "with_columns"           
    #> [57] "with_columns_seq"        "with_context"           
    #> [59] "with_row_index"

``` r
# see all private methods (not intended for regular use)
ls(.pr$LazyFrame)
```

    #>  [1] "clone_in_rust"           "collect"                
    #>  [3] "collect_in_background"   "debug_plan"             
    #>  [5] "describe_optimized_plan" "describe_plan"          
    #>  [7] "drop"                    "drop_nulls"             
    #>  [9] "explode"                 "fetch"                  
    #> [11] "fill_nan"                "fill_null"              
    #> [13] "filter"                  "first"                  
    #> [15] "get_optimization_toggle" "group_by"               
    #> [17] "group_by_dynamic"        "join"                   
    #> [19] "join_asof"               "last"                   
    #> [21] "max"                     "mean"                   
    #> [23] "median"                  "melt"                   
    #> [25] "min"                     "print"                  
    #> [27] "profile"                 "quantile"               
    #> [29] "rename"                  "reverse"                
    #> [31] "rolling"                 "schema"                 
    #> [33] "select"                  "select_seq"             
    #> [35] "set_optimization_toggle" "shift"                  
    #> [37] "shift_and_fill"          "sink_csv"               
    #> [39] "sink_ipc"                "sink_json"              
    #> [41] "sink_parquet"            "slice"                  
    #> [43] "sort_by_exprs"           "std"                    
    #> [45] "sum"                     "tail"                   
    #> [47] "to_dot"                  "unique"                 
    #> [49] "unnest"                  "var"                    
    #> [51] "with_columns"            "with_columns_seq"       
    #> [53] "with_context"            "with_row_index"

``` r
# Practical example ##
# First writing R iris dataset to disk, to illustrte a difference
temp_filepath = tempfile()
write.csv(iris, temp_filepath, row.names = FALSE)

# Following example illustrates 2 ways to obtain a LazyFrame

# The-Okay-way: convert an in-memory DataFrame to LazyFrame

# eager in-mem R data.frame
Rdf = read.csv(temp_filepath)

# eager in-mem polars DataFrame
Pdf = as_polars_df(Rdf)

# lazy frame starting from in-mem DataFrame
Ldf_okay = Pdf$lazy()

# The-Best-Way:  LazyFrame created directly from a data source is best...
Ldf_best = pl$scan_csv(temp_filepath)

# ... as if to e.g. filter the LazyFrame, that filtering also caleld predicate will be
# pushed down in the executation stack to the csv_reader, and thereby only bringing into
# memory the rows matching to filter.
# apply filter:
filter_expr = pl$col("Species") == "setosa" # get only rows where Species is setosa
Ldf_okay = Ldf_okay$filter(filter_expr) # overwrite LazyFrame with new
Ldf_best = Ldf_best$filter(filter_expr)

# the non optimized plans are similar, on entire in-mem csv, apply filter
Ldf_okay$describe_plan()
```

    #> FILTER [(col("Species")) == (String(setosa))] FROM
    #> DF ["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]; PROJECT */5 COLUMNS; SELECTION: "None"

``` r
Ldf_best$describe_plan()
```

    #> FILTER [(col("Species")) == (String(setosa))] FROM
    #> 
    #>   Csv SCAN /tmp/RtmpOnFq4Y/filea81d5d2f7f1a
    #>   PROJECT */5 COLUMNS

``` r
# NOTE For Ldf_okay, the full time to load csv alrady paid when creating Rdf and Pdf

# The optimized plan are quite different, Ldf_best will read csv and perform filter simultaneously
Ldf_okay$describe_optimized_plan()
```

    #> DF ["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]; PROJECT */5 COLUMNS; SELECTION: "[(col(\"Species\")) == (String(setosa))]"

``` r
Ldf_best$describe_optimized_plan()
```

    #> 
    #>   Csv SCAN /tmp/RtmpOnFq4Y/filea81d5d2f7f1a
    #>   PROJECT */5 COLUMNS
    #>   SELECTION: [(col("Species")) == (String(setosa))]

``` r
# To acquire result in-mem use $colelct()
Pdf_okay = Ldf_okay$collect()
Pdf_best = Ldf_best$collect()


# verify tables would be the same
all.equal(
  Pdf_okay$to_data_frame(),
  Pdf_best$to_data_frame()
)
```

    #> [1] TRUE

``` r
# a user might write it as a one-liner like so:
Pdf_best2 = pl$scan_csv(temp_filepath)$filter(pl$col("Species") == "setosa")
```
