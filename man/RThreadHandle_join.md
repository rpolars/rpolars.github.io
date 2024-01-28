

# Join a RThreadHandle

[**Source code**](https://github.com/pola-rs/r-polars/tree/1fd6c01b862685c50e295d9b2ef690a69c3a7963/R/rbackground.R#L85)

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
