
# Any polars class object is made of this

## Description

One SEXP of Rtype: "externalptr" + a class attribute

## Details

<ul>
<li>

<code>object$method()</code> calls are facilitated by a
<code style="white-space: pre;">$.ClassName</code>- s3method see
‘R/after-wrappers.R’

</li>
<li>

Code completion is facilitated by
<code>.DollarNames.ClassName</code>-s3method see
e.g. ’R/dataframe\_\_frame.R’

</li>
<li>

Implementation of property-methods as DataFrame_columns() and syntax
checking is an extension to
<code style="white-space: pre;">$.ClassName</code> See function
macro_add_syntax_check_to_class().

</li>
</ul>

## Value

not applicable

## Examples

``` r
library(polars)

# all a polars object is only made of:
some_polars_object = pl$DataFrame(iris)
str(some_polars_object) # External Pointer tagged with a class attribute.
```

    #> Class 'RPolarsDataFrame' <externalptr>

``` r
# All state is stored on rust side.

# The single exception from the rule is class "GroupBy", where objects also have
# two private attributes "groupby_input" and "maintain_order".
str(pl$DataFrame(iris)$group_by("Species"))
```

    #> Class 'RPolarsGroupBy' <externalptr> 
    #>  - attr(*, "private")=List of 2
    #>   ..$ groupby_input :List of 1
    #>   .. ..$ : chr "Species"
    #>   ..$ maintain_order: logi FALSE
