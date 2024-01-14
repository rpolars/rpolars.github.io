
# Inner workings of the DataFrame-class

## Description

The <code>DataFrame</code>-class is simply two environments of
respectively the public and private methods/function calls to the polars
Rust side. The instantiated <code>DataFrame</code>-object is an
<code>externalptr</code> to a low-level Rust polars DataFrame object.

The S3 method <code>.DollarNames.RPolarsDataFrame</code> exposes all
public <code style="white-space: pre;">$foobar()</code>-methods which
are callable onto the object. Most methods return another
<code>DataFrame</code>- class instance or similar which allows for
method chaining. This class system could be called "environment classes"
(in lack of a better name) and is the same class system
<code>extendr</code> provides, except here there are both a public and
private set of methods. For implementation reasons, the private methods
are external and must be called from
<code>.pr$DataFrame$methodname()</code>. Also, all private methods must
take any <code>self</code> as an argument, thus they are pure functions.
Having the private methods as pure functions solved/simplified
self-referential complications.

## Details

Check out the source code in
<a href="https://github.com/pola-rs/r-polars/blob/main/R/dataframe__frame.R">R/dataframe_frame.R</a>
to see how public methods are derived from private methods. Check out
<a href="https://github.com/pola-rs/r-polars/blob/main/R/extendr-wrappers.R">extendr-wrappers.R</a>
to see the <code>extendr</code>-auto-generated methods. These are moved
to <code>.pr</code> and converted into pure external functions in
<a href="https://github.com/pola-rs/r-polars/blob/main/R/after-wrappers.R">after-wrappers.R</a>.
In
<a href="https://github.com/pola-rs/r-polars/blob/main/R/zzz.R">zzz.R</a>
(named <code>zzz</code> to be last file sourced) the
<code>extendr</code>-methods are removed and replaced by any function
prefixed <code>DataFrame\_</code>.

## Value

Not applicable

## Examples

``` r
library(polars)

# see all public exported method names (normally accessed via a class
# instance with $)
ls(.pr$env$RPolarsDataFrame)
```

    #>  [1] "clone"            "columns"          "describe"         "drop"            
    #>  [5] "drop_in_place"    "drop_nulls"       "dtype_strings"    "dtypes"          
    #>  [9] "equals"           "estimated_size"   "explode"          "fill_nan"        
    #> [13] "fill_null"        "filter"           "first"            "get_column"      
    #> [17] "get_columns"      "glimpse"          "group_by"         "group_by_dynamic"
    #> [21] "head"             "height"           "join"             "join_asof"       
    #> [25] "last"             "lazy"             "limit"            "max"             
    #> [29] "mean"             "median"           "melt"             "min"             
    #> [33] "n_chunks"         "null_count"       "pivot"            "print"           
    #> [37] "quantile"         "rechunk"          "rename"           "reverse"         
    #> [41] "rolling"          "sample"           "schema"           "select"          
    #> [45] "shape"            "shift"            "shift_and_fill"   "slice"           
    #> [49] "sort"             "std"              "sum"              "tail"            
    #> [53] "to_data_frame"    "to_list"          "to_series"        "to_struct"       
    #> [57] "transpose"        "unique"           "unnest"           "var"             
    #> [61] "width"            "with_columns"     "with_row_count"   "write_csv"       
    #> [65] "write_json"       "write_ndjson"

``` r
# see all private methods (not intended for regular use)
ls(.pr$DataFrame)
```

    #>  [1] "clone_in_rust"             "columns"                  
    #>  [3] "default"                   "drop_all_in_place"        
    #>  [5] "drop_in_place"             "dtype_strings"            
    #>  [7] "dtypes"                    "equals"                   
    #>  [9] "estimated_size"            "export_stream"            
    #> [11] "from_arrow_record_batches" "get_column"               
    #> [13] "get_columns"               "lazy"                     
    #> [15] "melt"                      "n_chunks"                 
    #> [17] "new_with_capacity"         "null_count"               
    #> [19] "pivot_expr"                "print"                    
    #> [21] "rechunk"                   "sample_frac"              
    #> [23] "sample_n"                  "schema"                   
    #> [25] "select"                    "select_at_idx"            
    #> [27] "set_column_from_robj"      "set_column_from_series"   
    #> [29] "set_column_names_mut"      "shape"                    
    #> [31] "to_list"                   "to_list_tag_structs"      
    #> [33] "to_list_unwind"            "to_struct"                
    #> [35] "transpose"                 "unnest"                   
    #> [37] "with_columns"              "with_row_count"           
    #> [39] "write_csv"                 "write_json"               
    #> [41] "write_ndjson"

``` r
# make an object
df = pl$DataFrame(iris)


# use a public method/property
df$shape
```

    #> [1] 150   5

``` r
df2 = df

# use a private method, which has mutability
result = .pr$DataFrame$set_column_from_robj(df, 150:1, "some_ints")

# Column exists in both dataframes-objects now, as they are just pointers to
# the same object
# There are no public methods with mutability.
df$columns
```

    #> [1] "Sepal.Length" "Sepal.Width"  "Petal.Length" "Petal.Width"  "Species"     
    #> [6] "some_ints"

``` r
df2$columns
```

    #> [1] "Sepal.Length" "Sepal.Width"  "Petal.Length" "Petal.Width"  "Species"     
    #> [6] "some_ints"

``` r
# set_column_from_robj-method is fallible and returned a result which could
# be "ok" or an error.
# No public method or function will ever return a result.
# The `result` is very close to the same as output from functions decorated
# with purrr::safely.
# To use results on the R side, these must be unwrapped first such that
# potentially errors can be thrown. `unwrap(result)` is a way to communicate
# errors happening on the Rust side to the R side. `Extendr` default behavior
# is to use `panic!`(s) which would cause some unnecessarily confusing and
# some very verbose error messages on the inner workings of rust.
# `unwrap(result)` in this case no error, just a NULL because this mutable
# method does not return any ok-value.

# Try unwrapping an error from polars due to unmatching column lengths
err_result = .pr$DataFrame$set_column_from_robj(df, 1:10000, "wrong_length")
tryCatch(unwrap(err_result, call = NULL), error = \(e) cat(as.character(e)))
```

    #> Error in unwrap(err_result, call = NULL): could not find function "unwrap"
