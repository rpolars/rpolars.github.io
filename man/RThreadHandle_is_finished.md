

# Ask if RThreadHandle is finished?

[**Source code**](https://github.com/pola-rs/r-polars/tree/5765842071140bd7a822ebb4fd6b0ab652d73f0d/R/rbackground.R#L92)

## Description

Ask if RThreadHandle is finished?

## Usage

<pre><code class='language-R'>RThreadHandle_is_finished()
</code></pre>

## Value

trinary value: <code>TRUE</code> if finished, <code>FALSE</code> if not,
and <code>NULL</code> if the handle was exhausted with
<code>\<RThreadHandle\>$join()</code>.
