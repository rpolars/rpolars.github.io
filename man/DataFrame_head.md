
# Head of a DataFrame

[**Source code**](https://github.com/pola-rs/r-polars/tree/53c7d964901ed4a019998e89aff8c6d44691d793/R/dataframe__frame.R#L773)

## Description

Get the first <code>n</code> rows of the query.

## Usage

<pre><code class='language-R'>DataFrame_head(n)
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="DataFrame_head_:_n">n</code>
</td>
<td>
Positive number not larger than 2^32.
</td>
</tr>
</table>

## Details

Any number will converted to u32. Negative raises error.

## Value

DataFrame
