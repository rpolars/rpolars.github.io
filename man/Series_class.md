

# Inner workings of the Series-class

## Description

The <code>Series</code>-class is simply two environments of respectively
the public and private methods/function calls to the polars rust side.
The instantiated <code>Series</code>-object is an
<code>externalptr</code> to a lowlevel rust polars Series object. The
pointer address is the only statefullness of the Series object on the R
side. Any other state resides on the rust side. The S3 method
<code>.DollarNames.RPolarsSeries</code> exposes all public
<code style="white-space: pre;">$foobar()</code>-methods which are
callable onto the object. Most methods return another
<code>Series</code>-class instance or similar which allows for method
chaining. This class system in lack of a better name could be called
"environment classes" and is the same class system extendr provides,
except here there is both a public and private set of methods. For
implementation reasons, the private methods are external and must be
called from <code>.pr$Series$methodname()</code>, also all private
methods must take any self as an argument, thus they are pure functions.
Having the private methods as pure functions solved/simplified
self-referential complications.

## Details

Check out the source code in R/Series_frame.R how public methods are
derived from private methods. Check out extendr-wrappers.R to see the
extendr-auto-generated methods. These are moved to .pr and converted
into pure external functions in after-wrappers.R. In zzz.R (named zzz to
be last file sourced) the extendr-methods are removed and replaced by
any function prefixed <code>Series\_</code>.

## Active bindings

<h4>
flags
</h4>

<code style="white-space: pre;">$flags</code> returns a named list with
flag names and their values.

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

## Examples

``` r
library(polars)

pl$show_all_public_methods("RPolarsSeries")
```

    #> 
    #> 
    #>     RPolarsSeries class methods, access via object$method() ( environment ):
    #> 
    #>        RPolarsSeries ( environment ):
    #>           [ abs ; function ]
    #>           [ add ; function ]
    #>           [ alias ; function ]
    #>           [ all ; function ]
    #>           [ any ; function ]
    #>           [ append ; function ]
    #>           [ arg_max ; function ]
    #>           [ arg_min ; function ]
    #>           [ ceil ; function ]
    #>           [ chunk_lengths ; function ]
    #>           [ clone ; function ]
    #>           [ compare ; function ]
    #>           [ cum_sum ; function ]
    #>           [ div ; function ]
    #>           [ dtype ; property function ]
    #>           [ equals ; function ]
    #>           [ expr ; property function ]
    #>           [ flags ; property function ]
    #>           [ floor ; function ]
    #>           [ is_numeric ; function ]
    #>           [ is_sorted ; function ]
    #>           [ len ; function ]
    #>           [ list ; property function ]
    #>           [ map_elements ; function ]
    #>           [ max ; function ]
    #>           [ mean ; function ]
    #>           [ median ; function ]
    #>           [ min ; function ]
    #>           [ mul ; function ]
    #>           [ n_unique ; function ]
    #>           [ name ; property function ]
    #>           [ print ; function ]
    #>           [ rem ; function ]
    #>           [ rename ; function ]
    #>           [ rep ; function ]
    #>           [ set_sorted ; function ]
    #>           [ shape ; property function ]
    #>           [ sort ; function ]
    #>           [ std ; function ]
    #>           [ sub ; function ]
    #>           [ sum ; function ]
    #>           [ to_frame ; function ]
    #>           [ to_lit ; function ]
    #>           [ to_r ; function ]
    #>           [ to_r_list ; function ]
    #>           [ to_r_vector ; function ]
    #>           [ to_vector ; function ]
    #>           [ value_counts ; function ]
    #>           [ var ; function ]

``` r
# see all private methods (not intended for regular use)
ls(.pr$Series)
```

    #>  [1] "abs"                         "add"                        
    #>  [3] "alias"                       "all"                        
    #>  [5] "any"                         "append_mut"                 
    #>  [7] "arg_max"                     "arg_min"                    
    #>  [9] "ceil"                        "chunk_lengths"              
    #> [11] "clone"                       "compare"                    
    #> [13] "cum_sum"                     "div"                        
    #> [15] "dtype"                       "equals"                     
    #> [17] "fast_explode_flag"           "floor"                      
    #> [19] "from_arrow_array_robj"       "from_arrow_array_stream_str"
    #> [21] "get_fmt"                     "is_sorted"                  
    #> [23] "is_sorted_flag"              "is_sorted_reverse_flag"     
    #> [25] "len"                         "map_elements"               
    #> [27] "max"                         "mean"                       
    #> [29] "median"                      "min"                        
    #> [31] "mul"                         "n_unique"                   
    #> [33] "name"                        "new"                        
    #> [35] "panic"                       "print"                      
    #> [37] "rem"                         "rename_mut"                 
    #> [39] "rep"                         "set_sorted_mut"             
    #> [41] "shape"                       "sleep"                      
    #> [43] "sort_mut"                    "std"                        
    #> [45] "sub"                         "sum"                        
    #> [47] "to_fmt_char"                 "to_frame"                   
    #> [49] "to_r"                        "value_counts"               
    #> [51] "var"

``` r
# make an object
s = pl$Series(c(1:3, 1L))

# use a public method/property
s$shape
```

    #> [1] 4 1

``` r
# show flags
s$sort()$flags
```

    #> $SORTED_ASC
    #> [1] TRUE
    #> 
    #> $SORTED_DESC
    #> [1] FALSE

``` r
# use a private method (mutable append not allowed in public api)
s_copy = s
.pr$Series$append_mut(s, pl$Series(5:1))
```

    #> $ok
    #> NULL
    #> 
    #> $err
    #> NULL
    #> 
    #> attr(,"class")
    #> [1] "extendr_result"

``` r
identical(s_copy$to_r(), s$to_r()) # s_copy was modified when s was modified
```

    #> [1] TRUE
