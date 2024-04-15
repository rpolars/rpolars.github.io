

# Polars code completion

[**Source code**](https://github.com/pola-rs/r-polars/tree/d562252dbb77de7e06ca3e6150d74a2c709763bc/R/autocompletion.R#L47)

## Description

Polars code completion

## Usage

<pre><code class='language-R'>polars_code_completion_activate(
  mode = c("auto", "rstudio", "native"),
  verbose = TRUE
)

polars_code_completion_deactivate()
</code></pre>

## Arguments

<table>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="polars_code_completion_activate_:_mode">mode</code>
</td>
<td>
One of <code>“auto”</code>, <code>“rstudio”</code>, or
<code>“native”</code>. Automatic mode picks <code>“rstudio”</code> if
<code>.Platform$GUI</code> is <code>“RStudio”</code>.
<code>“native”</code> registers a custom line buffer completer with
<code>utils:::rc.getOption(“custom.completer”)</code>.
<code>“rstudio”</code> modifies RStudio code internal
<code>.DollarNames</code> and function args completion, as the IDE does
not behave well with
<code>utils:::rc.getOption(“custom.completer”)</code>.
</td>
</tr>
<tr>
<td style="white-space: nowrap; font-family: monospace; vertical-align: top">
<code id="polars_code_completion_activate_:_verbose">verbose</code>
</td>
<td>
Print message of what mode is started.
</td>
</tr>
</table>

## Details

Polars code completion has one implementation for a native terminal via
<code>utils:::rc.getOption(“custom.completer”)</code> and one for
Rstudio by intercepting Rstudio internal functions
<code>.rs.getCompletionsFunction</code> &
<code>.rs.getCompletionsDollar</code> in the loaded session environment
<code>tools:rstudio</code>. Therefore, any error or slowness in the
completion is likely to come from r-polars implementation.

Either completers will evaluate the full line-buffer to decide what
methods are available. Pressing tab will literally evaluate
left-hand-side with any following side. This works swiftly for the
polars lazy API, but it can take some time for the eager API depending
on the size of the data and of the query.

## Examples

``` r
library(polars)

if (interactive()) {
  # activate completion
  polars_code_completion_activate()

  # method / property completion for chained expressions
  # add a $ and press tab to see methods of LazyFrame
  pl$LazyFrame(iris)

  # Arg + column-name completion
  # press tab inside group_by() to see args and/or column names.
  pl$LazyFrame(iris)$group_by()

  # deactivate like this or restart R session
  polars_code_completion_deactivate()
}
```
