

# Get and reset polars options

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/polars_options.R#L159)

## Description

<code>polars_options()</code> returns a list of options for polars.
Options can be set with <code>options()</code>. Note that
<strong>options must be prefixed with "polars."</strong>, e.g to modify
the option <code>strictly_immutable</code> you need to pass
<code>options(polars.strictly_immutable =)</code>. See below for a
description of all options.

<code>polars_options_reset()</code> brings all polars options back to
their default value.

## Usage

<pre><code class='language-R'>polars_options()

polars_options_reset()
</code></pre>

## Details

The following options are available (in alphabetical order, with the
default value in parenthesis):

<ul>
<li>

<code>debug_polars</code> (<code>FALSE</code>): Print additional
information to debug Polars.

</li>
<li>

<code>do_not_repeat_call</code> (<code>FALSE</code>): Do not print the
call causing the error in error messages. The default is to show them.

</li>
<li>

<code>int64_conversion</code> (<code>“double”</code>): How should Int64
values be handled when converting a polars object to R?

<ul>
<li>

<code>“double”</code> converts the integer values to double.

</li>
<li>

<code>“bit64”</code> uses <code>bit64::as.integer64()</code> to do the
conversion (requires the package <code>bit64</code> to be attached).

</li>
<li>

<code>“string”</code> converts Int64 values to character.

</li>
</ul>
</li>
<li>

<code>limit_max_threads</code>
(<code>!polars_info()$features$disable_limit_max_threads</code>): See
<code>?pl_threadpool_size</code> for details. This option should be set
before the package is loaded.

</li>
<li>

<code>maintain_order</code> (<code>FALSE</code>): Default for all
<code>maintain_order</code> options (present in
<code style="white-space: pre;">$group_by()</code> or
<code style="white-space: pre;">$unique()</code> for example).

</li>
<li>

<code>no_messages</code> (<code>FALSE</code>): Hide messages.

</li>
<li>

<code>rpool_cap</code>: The maximum number of R sessions that can be
used to process R code in the background. See the section "About pool
options" below.

</li>
<li>

<code>strictly_immutable</code> (<code>TRUE</code>): Keep polars
strictly immutable. Polars/arrow is in general pro "immutable objects".
Immutability is also classic in R. To mimic the Python-polars API, set
this to <code>FALSE.</code>

</li>
</ul>

## Value

<code>polars_options()</code> returns a named list where the names are
option names and values are option values.

<code>polars_options_reset()</code> doesn’t return anything.

## About pool options

<code>polars_options()$rpool_active</code> indicates the number of R
sessions already spawned in pool.
<code>polars_options()$rpool_cap</code> indicates the maximum number of
new R sessions that can be spawned. Anytime a polars thread worker needs
a background R session specifically to run R code embedded in a query
via <code>$map_batches(…, in_background = TRUE)</code> or
<code>$map_elements(…, in_background = TRUE)</code>, it will obtain any
R session idling in rpool, or spawn a new R session (process) and add it
to the rpool if <code>rpool_cap</code> is not already reached. If
<code>rpool_cap</code> is already reached, the thread worker will sleep
until an R session is idling.

Background R sessions communicate via polars arrow IPC (series/vectors)
or R serialize + shared memory buffers via the rust crate
<code>ipc-channel</code>. Multi-process communication has overhead
because all data must be serialized/de-serialized and sent via buffers.
Using multiple R sessions will likely only give a speed-up in a
<code style="white-space: pre;">low io - high cpu</code> scenario.
Native polars query syntax runs in threads and have no overhead.

## Examples

``` r
library(polars)

options(polars.maintain_order = TRUE, polars.strictly_immutable = FALSE)
polars_options()
```

    #> Options:
    #> ========                         
    #> debug_polars        FALSE
    #> df_knitr_print       auto
    #> do_not_repeat_call  FALSE
    #> int64_conversion   double
    #> limit_max_threads   FALSE
    #> maintain_order       TRUE
    #> no_messages         FALSE
    #> rpool_active            0
    #> rpool_cap               4
    #> strictly_immutable  FALSE
    #> 
    #> See `?polars_options` for the definition of all options.

``` r
# option checks are run when calling polars_options(), not when setting
# options
options(polars.maintain_order = 42, polars.int64_conversion = "foobar")
tryCatch(
  polars_options(),
  error = function(e) print(e)
)
```

    #> <simpleError: Some polars options have an unexpected value:
    #> - maintain_order: input must be TRUE or FALSE.
    #> - int64_conversion: input must be one of "float", "string", "bit64".
    #> 
    #> More info at `?polars::polars_options`.>

``` r
# reset options to their default value
polars_options_reset()
```
