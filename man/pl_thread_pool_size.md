

# Get the number of threads in the Polars thread pool.

[**Source code**](https://github.com/pola-rs/r-polars/tree/main/R/polars_info.R#L103)

## Description

The threadpool size can be overridden by setting the
<code>POLARS_MAX_THREADS</code> environment variable before process
start. It cannot be modified once <code>polars</code> is loaded. It is
strongly recommended not to override this value as it will be set
automatically by the engine.

## Usage

<pre><code class='language-R'>pl_thread_pool_size()

pl_threadpool_size()
</code></pre>

## Details

For compatibility with CRAN, the threadpool size is set to 2 by default.
To disable this behavior and let the engine determine the threadpool
size, one of the following ways can be used:

<ul>
<li>

Enable the <code>disable_limit_max_threads</code> feature of the
library. This can be done by setting the feature flag when installing
the package. See the installation vignette (<code>vignette(“install”,
“polars”)</code>) for details.

</li>
<li>

Set the <code>polars.limit_max_threads</code> option to
<code>FALSE</code> with the <code>options()</code> function. Same as
setting the <code>POLARS_MAX_THREADS</code> environment variable, this
option must be set before loading the package.

</li>
</ul>

## Value

The number of threads

## Examples

``` r
library(polars)

pl$thread_pool_size()
```

    #> [1] 4
