

# Join a RThreadHandle

[**Source code**](https://github.com/pola-rs/r-polars/tree/mkdocs-matrial-search-preview/R/rbackground.R#L83)

## Description

Join a RThreadHandle

## Usage

<pre><code class='language-R'>RThreadHandle_join()
</code></pre>

## Details

method <code style="white-space: pre;">\<RThreadHandle\>$join()</code>:
will block until job is done and then return some value or raise an
error from the thread. Calling
<code style="white-space: pre;">\<RThreadHandle\>$join()</code> a second
time will raise an error because handle is already exhausted.

## Value

return value from background thread

## See Also

RThreadHandle_class
