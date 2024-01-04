
# Ask if RThreadHandle is finished?

[**Source code**](https://github.com/pola-rs/r-polars/tree/0580dbe189881934960c63979bf59fc3448a21dc/R/rbackground.R#L94)

## Description

Ask if RThreadHandle is finished?

## Usage

<pre><code class='language-R'>RThreadHandle_is_finished()
</code></pre>

## Value

trinary value: <code>TRUE</code> if finished, <code>FALSE</code> if not,
and <code>NULL</code> if the handle was exhausted with
<code>\<RThreadHandle\>$join()</code>.
