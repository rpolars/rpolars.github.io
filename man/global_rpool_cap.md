

# Get/set global R session pool capacity (DEPRECATED)

## Description

Deprecated. Use polars_options() to get, and pl$set_options() to set.

## Usage

<pre><code class='language-R'>pl_get_global_rpool_cap()

pl_set_global_rpool_cap(n)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="n">n</code>
</td>
<td>
Integer, the capacity limit R sessions to process R code.
</td>
</tr>
</table>

## Details

Background R sessions communicate via polars arrow IPC (series/vectors)
or R serialize + shared memory buffers via the rust crate
<code>ipc-channel</code>. Multi-process communication has overhead
because all data must be serialized/de-serialized and sent via buffers.
Using multiple R sessions will likely only give a speed-up in a
<code style="white-space: pre;">low io - high cpu</code> scenario.
Native polars query syntax runs in threads and have no overhead. Polars
has as default double as many thread workers as cores. If any worker are
queuing for or using R sessions, other workers can still continue any
native polars parts as much as possible.

## Value

<code>polars_options()$rpool_cap</code> returns the capacity ("limit")
of co-running external R sessions / processes.
<code>polars_options()$rpool_active</code> is the number of R sessions
are already spawned in the pool. <code>rpool_cap</code> is the limit of
new R sessions to spawn. Anytime a polars thread worker needs a
background R session specifically to run R code embedded in a query via
<code>$map_batches(…, in_background = TRUE)</code> or
<code>$map_elements(…, in_background = TRUE)</code>, it will obtain any
R session idling in rpool, or spawn a new R session (process) if
<code>capacity</code> is not already reached. If <code>capacity</code>
is already reached, the thread worker will sleep and in a R job queue
until an R session is idle.

## Examples

``` r
library(polars)

default = polars_options()$rpool_cap |> print()
```

    #> [1] 4

``` r
options(polars.rpool_cap = 8)
polars_options()$rpool_cap
```

    #> [1] 8

``` r
options(polars.rpool_cap = default)
polars_options()$rpool_cap
```

    #> [1] 4
