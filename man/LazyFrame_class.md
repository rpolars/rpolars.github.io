

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

## Examples

``` r
library(polars)

# see all exported methods
ls(.pr$env$RPolarsLazyFrame)
```

    #>  [1] "clone"                   "collect"                
    #>  [3] "collect_in_background"   "columns"                
    #>  [5] "describe_optimized_plan" "describe_plan"          
    #>  [7] "drop"                    "drop_nulls"             
    #>  [9] "dtypes"                  "explode"                
    #> [11] "fetch"                   "fill_nan"               
    #> [13] "fill_null"               "filter"                 
    #> [15] "first"                   "get_optimization_toggle"
    #> [17] "group_by"                "group_by_dynamic"       
    #> [19] "head"                    "join"                   
    #> [21] "join_asof"               "last"                   
    #> [23] "limit"                   "max"                    
    #> [25] "mean"                    "median"                 
    #> [27] "melt"                    "min"                    
    #> [29] "print"                   "profile"                
    #> [31] "quantile"                "rename"                 
    #> [33] "reverse"                 "rolling"                
    #> [35] "schema"                  "select"                 
    #> [37] "set_optimization_toggle" "shift"                  
    #> [39] "shift_and_fill"          "sink_csv"               
    #> [41] "sink_ipc"                "sink_ndjson"            
    #> [43] "sink_parquet"            "slice"                  
    #> [45] "sort"                    "std"                    
    #> [47] "sum"                     "tail"                   
    #> [49] "unique"                  "unnest"                 
    #> [51] "var"                     "width"                  
    #> [53] "with_columns"            "with_context"           
    #> [55] "with_row_count"          "with_row_index"

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
    #> [33] "select"                  "select_str_as_lit"      
    #> [35] "set_optimization_toggle" "shift"                  
    #> [37] "shift_and_fill"          "sink_csv"               
    #> [39] "sink_ipc"                "sink_json"              
    #> [41] "sink_parquet"            "slice"                  
    #> [43] "sort_by_exprs"           "std"                    
    #> [45] "sum"                     "tail"                   
    #> [47] "unique"                  "unnest"                 
    #> [49] "var"                     "with_columns"           
    #> [51] "with_context"            "with_row_index"

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
    #>   Csv SCAN /tmp/RtmporRrhi/file7acf7e48b015
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
    #>   Csv SCAN /tmp/RtmporRrhi/file7acf7e48b015
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
