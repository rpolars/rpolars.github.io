

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
flags
</h4>

<code style="white-space: pre;">$flags</code> returns a nested list with
column names at the top level and column flags in each sublist.

Flags are used internally to avoid doing unnecessary computations, such
as sorting a variable that we know is already sorted. The number of
flags varies depending on the column type: columns of type
<code>array</code> and <code>list</code> have the flags
<code>SORTED_ASC</code>, <code>SORTED_DESC</code>, and
<code>FAST_EXPLODE</code>, while other column types only have the former
two.

<ul>
<li>

<code>SORTED_ASC</code> is set to <code>TRUE</code> when we sort a
column in increasing order, so that we can use this information later on
to avoid re-sorting it.

</li>
<li>

<code>SORTED_DESC</code> is similar but applies to sort in decreasing
order.

</li>
</ul>
<h4>
height
</h4>

<code style="white-space: pre;">$height</code> returns the number of
rows in the DataFrame.

<h4>
schema
</h4>

<code style="white-space: pre;">$schema</code> returns a named list with
the data type of each column.

<h4>
shape
</h4>

<code style="white-space: pre;">$shape</code> returns a numeric vector
of length two with the number of rows and the number of columns.

<h4>
width
</h4>

<code style="white-space: pre;">$width</code> returns the number of
columns in the DataFrame.

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
    #> [13] "fill_null"        "filter"           "first"            "flags"           
    #> [17] "get_column"       "get_columns"      "glimpse"          "group_by"        
    #> [21] "group_by_dynamic" "head"             "height"           "join"            
    #> [25] "join_asof"        "last"             "lazy"             "limit"           
    #> [29] "max"              "mean"             "median"           "melt"            
    #> [33] "min"              "n_chunks"         "null_count"       "pivot"           
    #> [37] "print"            "quantile"         "rechunk"          "rename"          
    #> [41] "reverse"          "rolling"          "sample"           "schema"          
    #> [45] "select"           "shape"            "shift"            "shift_and_fill"  
    #> [49] "slice"            "sort"             "std"              "sum"             
    #> [53] "tail"             "to_data_frame"    "to_list"          "to_series"       
    #> [57] "to_struct"        "transpose"        "unique"           "unnest"          
    #> [61] "var"              "width"            "with_columns"     "with_row_count"  
    #> [65] "with_row_index"   "write_csv"        "write_json"       "write_ndjson"    
    #> [69] "write_parquet"

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
    #> [37] "with_columns"              "with_row_index"           
    #> [39] "write_csv"                 "write_json"               
    #> [41] "write_ndjson"              "write_parquet"

``` r
# make an object
df = as_polars_df(iris)

# call an active binding
df$shape
```

    #> [1] 150   5

``` r
# use a private method, which has mutability
result = .pr$DataFrame$set_column_from_robj(df, 150:1, "some_ints")

# Column exists in both dataframes-objects now, as they are just pointers to
# the same object
# There are no public methods with mutability.
df2 = df

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
# Show flags
df$sort("Sepal.Length")$flags
```

    #> $Sepal.Length
    #> $Sepal.Length$SORTED_ASC
    #> [1] TRUE
    #> 
    #> $Sepal.Length$SORTED_DESC
    #> [1] FALSE
    #> 
    #> 
    #> $Sepal.Width
    #> $Sepal.Width$SORTED_ASC
    #> [1] FALSE
    #> 
    #> $Sepal.Width$SORTED_DESC
    #> [1] FALSE
    #> 
    #> 
    #> $Petal.Length
    #> $Petal.Length$SORTED_ASC
    #> [1] FALSE
    #> 
    #> $Petal.Length$SORTED_DESC
    #> [1] FALSE
    #> 
    #> 
    #> $Petal.Width
    #> $Petal.Width$SORTED_ASC
    #> [1] FALSE
    #> 
    #> $Petal.Width$SORTED_DESC
    #> [1] FALSE
    #> 
    #> 
    #> $Species
    #> $Species$SORTED_ASC
    #> [1] FALSE
    #> 
    #> $Species$SORTED_DESC
    #> [1] FALSE
    #> 
    #> 
    #> $some_ints
    #> $some_ints$SORTED_ASC
    #> [1] FALSE
    #> 
    #> $some_ints$SORTED_DESC
    #> [1] FALSE

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
