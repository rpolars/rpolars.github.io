

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

## Sub-namespaces

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
expr
</h4>

<code style="white-space: pre;">$expr</code> works as a workaround for
applying arbitrary Expr methods to the Series class object, which means
that this is a shortcut works like
<code style="white-space: pre;">pl$select(s)$select(pl$col(s$name)$\<Expr
method\>)$to_series(0)</code>. This subnamespace is experimental.

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
methods.

## Examples

``` r
library(polars)

# make a Series
s = pl$Series(c(1:3, 1L))

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
# use subnamespaces
pl$Series(list(3:1, 1:2, NULL))$list$first()
```

    #> polars Series: shape: (3,)
    #> Series: '' [i32]
    #> [
    #>  3
    #>  1
    #>  null
    #> ]

``` r
pl$Series(c(1, NA, 2))$str$concat("-")
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
    #>           [ any ; function ]
    #>           [ append ; function ]
    #>           [ arg_max ; function ]
    #>           [ arg_min ; function ]
    #>           [ arr ; property function ]
    #>           [ bin ; property function ]
    #>           [ cat ; property function ]
    #>           [ ceil ; function ]
    #>           [ chunk_lengths ; function ]
    #>           [ clone ; function ]
    #>           [ compare ; function ]
    #>           [ cum_sum ; function ]
    #>           [ div ; function ]
    #>           [ dt ; property function ]
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
    #>           [ str ; property function ]
    #>           [ struct ; property function ]
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
