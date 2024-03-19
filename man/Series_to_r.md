

# Convert Series to R vector or list

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/series__series.R#L506)

## Description

<code style="white-space: pre;">$to_r()</code> automatically returns an
R vector or list based on the Polars DataType. It is possible to force
the output type by using
<code style="white-space: pre;">$to_vector()</code> or
<code style="white-space: pre;">$to_list()</code>.

## Usage

<pre><code class='language-R'>Series_to_r(int64_conversion = polars_options()\$int64_conversion)

Series_to_vector(int64_conversion = polars_options()\$int64_conversion)

Series_to_list(int64_conversion = polars_options()\$int64_conversion)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="Series_to_r_:_int64_conversion">int64_conversion</code>
</td>
<td>

How should Int64 values be handled when converting a polars object to R?

<ul>
<li>

<code>“double”</code> (default) converts the integer values to double.

</li>
<li>

<code>“bit64”</code> uses <code>bit64::as.integer64()</code> to do the
conversion (requires the package <code>bit64</code> to be attached).

</li>
<li>

<code>“string”</code> converts Int64 values to character.

</li>
</ul>
</td>
</tr>
</table>

## Value

R list or vector

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
non_existent_time = pl\$Series("2020-03-08 02:00:00")\$str\$strptime(pl\$Datetime(), "%F %T")

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

# Series with non-list type
series_vec = pl$Series(letters[1:3])

series_vec$to_r() # as vector because Series DataType is not list (is String)
```

    #> [1] "a" "b" "c"

``` r
series_vec$to_list() # implicit call as.list(), convert to list
```

    #> [[1]]
    #> [1] "a"
    #> 
    #> [[2]]
    #> [1] "b"
    #> 
    #> [[3]]
    #> [1] "c"

``` r
series_vec$to_vector() # implicit call unlist(), same as to_r() as already vector
```

    #> [1] "a" "b" "c"

``` r
# make a Series with nested lists
series_list = pl$Series(
  list(
    list(c(1:5, NA_integer_)),
    list(1:2, NA_integer_)
  )
)
series_list
```

    #> polars Series: shape: (2,)
    #> Series: '' [list[list[i32]]]
    #> [
    #>  [[1, 2, … null]]
    #>  [[1, 2], [null]]
    #> ]

``` r
series_list$to_r() # as list because Series DataType is list
```

    #> [[1]]
    #> [[1]][[1]]
    #> [1]  1  2  3  4  5 NA
    #> 
    #> 
    #> [[2]]
    #> [[2]][[1]]
    #> [1] 1 2
    #> 
    #> [[2]][[2]]
    #> [1] NA

``` r
series_list$to_list() # implicit call as.list(), same as to_r() as already list
```

    #> [[1]]
    #> [[1]][[1]]
    #> [1]  1  2  3  4  5 NA
    #> 
    #> 
    #> [[2]]
    #> [[2]][[1]]
    #> [1] 1 2
    #> 
    #> [[2]][[2]]
    #> [1] NA

``` r
series_list$to_vector() # implicit call unlist(), append into a vector
```

    #> [1]  1  2  3  4  5 NA  1  2 NA
