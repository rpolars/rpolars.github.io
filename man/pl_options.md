

# Set polars options

## Description

\[DEPRECATED\] Please use <code>options()</code> to set options,
<code>polars_options()</code> to get them, and
<code>polars_options_reset()</code> to reset them. See the documentation
of <code>polars_options()</code> for details.

## Usage

<pre><code class='language-R'>pl_set_options(
  ...,
  strictly_immutable = TRUE,
  maintain_order = FALSE,
  do_not_repeat_call = FALSE,
  debug_polars = FALSE,
  no_messages = FALSE,
  rpool_cap = 4,
  int64_conversion = c("bit64", "double", "string")
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
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="pl_set_options_:_int64_conversion">int64_conversion</code>
</td>
<td>

How should Int64 values be handled when converting a polars object to R?

<ul>
<li>

<code>“double”</code> (default) converts the integer values to double.

</li>
<li>

<code>“bit64”</code> uses <code>bit64::as.integer64()</code> to do the
conversion (requires the package <code>bit64</code> to be attached).

</li>
<li>

<code>“string”</code> converts Int64 values to character.

</li>
</ul>
</td>
</tr>
</table>

## Value

<code>polars_options()</code> returns a named list with the value
(<code>TRUE</code> or <code>FALSE</code>) of each option.

<code>pl$set_options()</code> silently modifies the options values.

<code>pl$reset_options()</code> silently resets the options to their
default values.
