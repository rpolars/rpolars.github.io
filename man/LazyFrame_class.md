
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
a <code>Frame</code>. To convert use <code>DataFrame_object$lazy() -\>
LazyFrame_object</code> and <code>LazyFrame_object$collect() -\>
DataFrame_object</code>. You can also create a <code>LazyFrame</code>
directly with <code>pl$LazyFrame()</code>. This is quite similar to the
lazy-collect syntax of the dplyrpackage to interact with database
connections such as SQL variants. Most SQL databases would be able to
perform the same optimizations as polars such Predicate Pushdown and
Projection. However polars can interact and optimize queries with both
SQL DBs and other data sources such parquet files simultaneously. (#TODO
implement r-polars SQL ;).

## Details

Check out the source code in R/LazyFrame\_*lazy.R how public methods are
derived from private methods. Check out extendr-wrappers.R to see the
extendr-auto-generated methods. These are moved to <code>.pr</code> and
converted into pure external functions in after-wrappers.R. In zzz.R
(named zzz to be last file sourced) the extendr-methods are removed and
replaced by any function prefixed <code>LazyFrame*</code>.

## Value

not applicable

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
    #> [55] "with_row_count"

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
    #> [21] "limit"                   "max"                    
    #> [23] "mean"                    "median"                 
    #> [25] "melt"                    "min"                    
    #> [27] "print"                   "profile"                
    #> [29] "quantile"                "rename"                 
    #> [31] "reverse"                 "rolling"                
    #> [33] "schema"                  "select"                 
    #> [35] "select_str_as_lit"       "set_optimization_toggle"
    #> [37] "shift"                   "shift_and_fill"         
    #> [39] "sink_csv"                "sink_ipc"               
    #> [41] "sink_json"               "sink_parquet"           
    #> [43] "slice"                   "sort_by_exprs"          
    #> [45] "std"                     "sum"                    
    #> [47] "tail"                    "unique"                 
    #> [49] "unnest"                  "var"                    
    #> [51] "with_columns"            "with_context"           
    #> [53] "with_row_count"

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
Pdf = pl$DataFrame(Rdf)

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
    #>   Csv SCAN /tmp/RtmpnuMcPR/file71aa5ec842f3
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
    #>   Csv SCAN /tmp/RtmpnuMcPR/file71aa5ec842f3
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
