

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
dtype
</h4>

<code style="white-space: pre;">$dtype</code> returns the data type of
the Series.

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
<h4>
name
</h4>

<code style="white-space: pre;">$name</code> returns the name of the
Series.

<h4>
shape
</h4>

<code style="white-space: pre;">$shape</code> returns a numeric vector
of length two with the number of length of the Series and width of the
Series (always 1).

## Expression methods

Series stores most of all Expr methods.

Some of these are stored in sub-namespaces.

<h4>
arr
</h4>

<code style="white-space: pre;">$arr</code> stores all array related
methods.

<h4>
bin
</h4>

<code style="white-space: pre;">$bin</code> stores all binary related
methods.

<h4>
cat
</h4>

<code style="white-space: pre;">$cat</code> stores all categorical
related methods.

<h4>
dt
</h4>

<code style="white-space: pre;">$dt</code> stores all temporal related
methods.

<h4>
list
</h4>

<code style="white-space: pre;">$list</code> stores all list related
methods.

<h4>
str
</h4>

<code style="white-space: pre;">$str</code> stores all string related
methods.

<h4>
struct
</h4>

<code style="white-space: pre;">$struct</code> stores all struct related
methods and active bindings.

Active bindings specific to Series:

<ul>
<li>

<code style="white-space: pre;">$struct$fields</code>: Returns a
character vector of the fields in the struct.

</li>
</ul>

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

# make a Series
s = as_polars_series(c(1:3, 1L))

# call an active binding
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
# use Expr method
s$cos()
```

    #> polars Series: shape: (4,)
    #> Series: '' [f64]
    #> [
    #>  0.540302
    #>  -0.416147
    #>  -0.989992
    #>  0.540302
    #> ]

``` r
# use Expr method in subnamespaces
as_polars_series(list(3:1, 1:2, NULL))$list$first()
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  3
    #>  1
    #>  null
    #> ]

``` r
as_polars_series(c(1, NA, 2))$str$concat("-")
```

    #> polars Series: shape: (1,)
    #> Series: '' [str]
    #> [
    #>  "1.0-2.0"
    #> ]

``` r
s = pl$date_range(
  as.Date("2024-02-18"), as.Date("2024-02-24"),
  interval = "1d"
)$to_series()
s
```

    #> polars Series: shape: (7,)
    #> Series: '' [date]
    #> [
    #>  2024-02-18
    #>  2024-02-19
    #>  2024-02-20
    #>  2024-02-21
    #>  2024-02-22
    #>  2024-02-23
    #>  2024-02-24
    #> ]

``` r
s$dt$day()
```

    #> polars Series: shape: (7,)
    #> Series: '' [i8]
    #> [
    #>  18
    #>  19
    #>  20
    #>  21
    #>  22
    #>  23
    #>  24
    #> ]

``` r
# Other active bindings in subnamespaces
as_polars_series(data.frame(a = 1:2, b = 3:4))$struct$fields
```

    #> [1] "a" "b"

``` r
# show all available methods for Series
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
    #>           [ and ; function ]
    #>           [ any ; function ]
    #>           [ append ; function ]
    #>           [ approx_n_unique ; function ]
    #>           [ arccos ; function ]
    #>           [ arccosh ; function ]
    #>           [ arcsin ; function ]
    #>           [ arcsinh ; function ]
    #>           [ arctan ; function ]
    #>           [ arctanh ; function ]
    #>           [ arg_max ; function ]
    #>           [ arg_min ; function ]
    #>           [ arg_sort ; function ]
    #>           [ arg_unique ; function ]
    #>           [ arr ; property function ]
    #>           [ backward_fill ; function ]
    #>           [ bin ; property function ]
    #>           [ bottom_k ; function ]
    #>           [ cast ; function ]
    #>           [ cat ; property function ]
    #>           [ ceil ; function ]
    #>           [ chunk_lengths ; function ]
    #>           [ clear ; function ]
    #>           [ clip ; function ]
    #>           [ clip_max ; function ]
    #>           [ clip_min ; function ]
    #>           [ clone ; function ]
    #>           [ compare ; function ]
    #>           [ cos ; function ]
    #>           [ cosh ; function ]
    #>           [ count ; function ]
    #>           [ cum_count ; function ]
    #>           [ cum_max ; function ]
    #>           [ cum_min ; function ]
    #>           [ cum_prod ; function ]
    #>           [ cum_sum ; function ]
    #>           [ cumulative_eval ; function ]
    #>           [ diff ; function ]
    #>           [ div ; function ]
    #>           [ dot ; function ]
    #>           [ drop_nans ; function ]
    #>           [ drop_nulls ; function ]
    #>           [ dt ; property function ]
    #>           [ dtype ; property function ]
    #>           [ entropy ; function ]
    #>           [ eq ; function ]
    #>           [ eq_missing ; function ]
    #>           [ equals ; function ]
    #>           [ ewm_mean ; function ]
    #>           [ ewm_std ; function ]
    #>           [ ewm_var ; function ]
    #>           [ exp ; function ]
    #>           [ explode ; function ]
    #>           [ extend_constant ; function ]
    #>           [ fill_nan ; function ]
    #>           [ fill_null ; function ]
    #>           [ filter ; function ]
    #>           [ first ; function ]
    #>           [ flags ; property function ]
    #>           [ flatten ; function ]
    #>           [ floor ; function ]
    #>           [ floor_div ; function ]
    #>           [ forward_fill ; function ]
    #>           [ gather ; function ]
    #>           [ gather_every ; function ]
    #>           [ gt ; function ]
    #>           [ gt_eq ; function ]
    #>           [ hash ; function ]
    #>           [ head ; function ]
    #>           [ implode ; function ]
    #>           [ interpolate ; function ]
    #>           [ is_between ; function ]
    #>           [ is_duplicated ; function ]
    #>           [ is_finite ; function ]
    #>           [ is_first_distinct ; function ]
    #>           [ is_in ; function ]
    #>           [ is_infinite ; function ]
    #>           [ is_last_distinct ; function ]
    #>           [ is_nan ; function ]
    #>           [ is_not_nan ; function ]
    #>           [ is_not_null ; function ]
    #>           [ is_null ; function ]
    #>           [ is_numeric ; function ]
    #>           [ is_sorted ; function ]
    #>           [ is_unique ; function ]
    #>           [ item ; function ]
    #>           [ kurtosis ; function ]
    #>           [ last ; function ]
    #>           [ len ; function ]
    #>           [ limit ; function ]
    #>           [ list ; property function ]
    #>           [ log ; function ]
    #>           [ log10 ; function ]
    #>           [ lower_bound ; function ]
    #>           [ lt ; function ]
    #>           [ lt_eq ; function ]
    #>           [ map_batches ; function ]
    #>           [ map_elements ; function ]
    #>           [ max ; function ]
    #>           [ mean ; function ]
    #>           [ median ; function ]
    #>           [ min ; function ]
    #>           [ mod ; function ]
    #>           [ mode ; function ]
    #>           [ mul ; function ]
    #>           [ n_chunks ; function ]
    #>           [ n_unique ; function ]
    #>           [ name ; property function ]
    #>           [ nan_max ; function ]
    #>           [ nan_min ; function ]
    #>           [ neq ; function ]
    #>           [ neq_missing ; function ]
    #>           [ not ; function ]
    #>           [ null_count ; function ]
    #>           [ or ; function ]
    #>           [ pct_change ; function ]
    #>           [ peak_max ; function ]
    #>           [ peak_min ; function ]
    #>           [ pow ; function ]
    #>           [ print ; function ]
    #>           [ product ; function ]
    #>           [ quantile ; function ]
    #>           [ rank ; function ]
    #>           [ rechunk ; function ]
    #>           [ reinterpret ; function ]
    #>           [ rename ; function ]
    #>           [ rep ; function ]
    #>           [ repeat_by ; function ]
    #>           [ replace ; function ]
    #>           [ reshape ; function ]
    #>           [ reverse ; function ]
    #>           [ rle ; function ]
    #>           [ rle_id ; function ]
    #>           [ rolling_max ; function ]
    #>           [ rolling_mean ; function ]
    #>           [ rolling_median ; function ]
    #>           [ rolling_min ; function ]
    #>           [ rolling_quantile ; function ]
    #>           [ rolling_skew ; function ]
    #>           [ rolling_std ; function ]
    #>           [ rolling_sum ; function ]
    #>           [ rolling_var ; function ]
    #>           [ round ; function ]
    #>           [ sample ; function ]
    #>           [ search_sorted ; function ]
    #>           [ set_sorted ; function ]
    #>           [ shape ; property function ]
    #>           [ shift ; function ]
    #>           [ shift_and_fill ; function ]
    #>           [ shrink_dtype ; function ]
    #>           [ shuffle ; function ]
    #>           [ sign ; function ]
    #>           [ sin ; function ]
    #>           [ sinh ; function ]
    #>           [ skew ; function ]
    #>           [ slice ; function ]
    #>           [ sort ; function ]
    #>           [ sort_by ; function ]
    #>           [ sqrt ; function ]
    #>           [ std ; function ]
    #>           [ str ; property function ]
    #>           [ struct ; property function ]
    #>           [ sub ; function ]
    #>           [ sum ; function ]
    #>           [ tail ; function ]
    #>           [ tan ; function ]
    #>           [ tanh ; function ]
    #>           [ to_frame ; function ]
    #>           [ to_list ; function ]
    #>           [ to_lit ; function ]
    #>           [ to_physical ; function ]
    #>           [ to_r ; function ]
    #>           [ to_struct ; function ]
    #>           [ to_vector ; function ]
    #>           [ top_k ; function ]
    #>           [ unique ; function ]
    #>           [ unique_counts ; function ]
    #>           [ upper_bound ; function ]
    #>           [ value_counts ; function ]
    #>           [ var ; function ]
    #>           [ xor ; function ]
