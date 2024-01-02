
# Get the number of threads in the Polars thread pool.

[**Source code**](https://github.com/pola-rs/r-polars/tree/4c60e4ba5981c539b9639261157303d78f545b69/R/extendr-wrappers.R#L114)

## Description

The threadpool size can be overridden by setting the
<code>POLARS_MAX_THREADS</code> environment variable before process
start. (The thread pool is not behind a lock, so it cannot be modified
once set). It is strongly recommended not to override this value as it
will be set automatically by the engine.

## Usage

<pre><code class='language-R'>pl_threadpool_size()
</code></pre>

## Value

The number of threads

## Examples

``` r
library(polars)

pl$threadpool_size()
```

    #> [1] 4
