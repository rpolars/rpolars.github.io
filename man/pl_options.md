
# Set polars options

## Description

Get and set polars options. See sections "Value" and "Examples" below
for more details.

## Usage

<pre><code class='language-R'>pl_set_options(
  ...,
  strictly_immutable = TRUE,
  maintain_order = FALSE,
  do_not_repeat_call = FALSE,
  debug_polars = FALSE,
  no_messages = FALSE,
  rpool_cap = 4
)

pl_reset_options()
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_set_options_:_...">…</code>
</td>
<td>
Ignored.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_set_options_:_strictly_immutable">strictly_immutable</code>
</td>
<td>
Keep polars strictly immutable. Polars/arrow is in general pro
"immutable objects". Immutability is also classic in R. To mimic the
Python-polars API, set this to <code>FALSE.</code>
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_set_options_:_maintain_order">maintain_order</code>
</td>
<td>
Default for all <code>maintain_order</code> options (present in
<code style="white-space: pre;">$group_by()</code> or
<code style="white-space: pre;">$unique()</code> for example).
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_set_options_:_do_not_repeat_call">do_not_repeat_call</code>
</td>
<td>
Do not print the call causing the error in error messages. The default
(<code>FALSE</code>) is to show them.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_set_options_:_debug_polars">debug_polars</code>
</td>
<td>
Print additional information to debug Polars.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_set_options_:_no_messages">no_messages</code>
</td>
<td>
Hide messages.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_set_options_:_rpool_cap">rpool_cap</code>
</td>
<td>
The maximum number of R sessions that can be used to process R code in
the background. See Details.
</td>
</tr>
</table>

## Details

<code>pl$options$rpool_active</code> indicates the number of R sessions
already spawned in pool. <code>pl$options$rpool_cap</code> indicates the
maximum number of new R sessions that can be spawned. Anytime a polars
thread worker needs a background R session specifically to run R code
embedded in a query via <code style="white-space: pre;">$map_batches(…,
in_background = TRUE)</code> or
<code style="white-space: pre;">$map_elements(…, in_background =
TRUE)</code>, it will obtain any R session idling in rpool, or spawn a
new R session (process) and add it to the rpool if
<code>rpool_cap</code> is not already reached. If <code>rpool_cap</code>
is already reached, the thread worker will sleep until an R session is
idling.

Background R sessions communicate via polars arrow IPC (series/vectors)
or R serialize + shared memory buffers via the rust crate
<code>ipc-channel</code>. Multi-process communication has overhead
because all data must be serialized/de-serialized and sent via buffers.
Using multiple R sessions will likely only give a speed-up in a
<code style="white-space: pre;">low io - high cpu</code> scenario.
Native polars query syntax runs in threads and have no overhead.

## Value

<code>pl$options</code> returns a named list with the value
(<code>TRUE</code> or <code>FALSE</code>) of each option.

<code>pl$set_options()</code> silently modifies the options values.

<code>pl$reset_options()</code> silently resets the options to their
default values.

## Examples

``` r
library(polars)

pl$set_options(maintain_order = TRUE, strictly_immutable = FALSE)
pl$options
```

    #> $maintain_order
    #> [1] TRUE
    #> 
    #> $rpool_cap
    #> [1] 4
    #> 
    #> $do_not_repeat_call
    #> [1] FALSE
    #> 
    #> $strictly_immutable
    #> [1] FALSE
    #> 
    #> $rpool_active
    #> [1] 0
    #> 
    #> $debug_polars
    #> [1] FALSE
    #> 
    #> $no_messages
    #> [1] FALSE

``` r
# these options only accept booleans (TRUE or FALSE)
tryCatch(
  pl$set_options(strictly_immutable = 42),
  error = function(e) print(e)
)
```

    #> <RPolarsErr_error: Execution halted with the following contexts
    #>    0: In R: in pl$set_options
    #>    0: During function call [.main()]
    #>    1: The argument [strictly_immutable] caused an error
    #>    2: Got value [Rvalue: 42.0, Rsexp: Doubles, Rclass: ["numeric"]]
    #>    3: Input must be TRUE or FALSE
    #> >

``` r
# reset options to their default value
pl$reset_options()
```
