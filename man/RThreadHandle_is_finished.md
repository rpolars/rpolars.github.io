

# Ask if RThreadHandle is finished?

[**Source code**](https://github.com/pola-rs/r-polars/tree/f1aede4d7d7f090c98651365a4120a8232503a4d/R/rbackground.R#L94)

## Description

Ask if RThreadHandle is finished?

## Usage

<pre><code class='language-R'>RThreadHandle_is_finished()
</code></pre>

## Value

trinary value: <code>TRUE</code> if finished, <code>FALSE</code> if not,
and <code>NULL</code> if the handle was exhausted with
<code>\<RThreadHandle\>$join()</code>.
