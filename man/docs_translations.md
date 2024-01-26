

# Translation definitions across python, R and polars.

## Description

#Comments for how the R and python world translates into polars:

R and python are both high-level glue languages great for Data Science.
Rust is a pedantic low-level language with similar use cases as C and
C++. Polars is written in ~100k lines of rust and has a rust API.
Py-polars the python API for polars, is implemented as an interface with
the rust API. r-polars is very parallel to py-polars except it
interfaces with R. The performance and behavior are unexpectedly quite
similar as the ‘engine’ is the exact same rust code and data structures.

## Format

info

## Value

Not applicable

## Translation details

<h4>
R and the integerish
</h4>

R only has a native Int32 type, no Uint32, Int64, UInt64 , … types.
These days Int32 is getting a bit small, to refer to more rows than ~
2^31-1. There are packages which provide int64, but the most normal
hack’ is to just use floats as ‘integerish’. There is an unique float64
value for every integer up to about 2^52 which is plenty for all
practical concerns. Some polars methods may accept or return a floats
even though an integer ideally would be more accurate. Most R functions
intermix Int32 (integer) and Float64 (double) seamlessly.

<h4>
Missingness
</h4>

R has allocated a value in every vector type to signal missingness,
these are collectively called <code>NAs</code>. Polars uses a bool
bitmask to signal <code>NA</code>-like missing value and it is called
<code>Null</code> and <code>Nulls</code> in plural. Not to confuse with
R <code>NULL</code> (see paragraph below). Polars supports missingness
for any possible type as it kept separately in the bitmask. In python
lists the symbol <code>None</code> can carry a similar meaning. R
<code>NA</code> ~ polars <code>Null</code> ~ py-polars
<code style="white-space: pre;">\[None\]</code> (in a py list)

<h4>
Sorting and comparisons
</h4>

From writing a lot of tests for all implementations, it appears polars
does not have a fully consistent nor well documented behavior, when it
comes to comparisons and sorting of floats. Though some general thumb
rules do apply: Polars have chosen to define in sorting that
<code>Null</code> is a value lower than <code>-Inf</code> as in
<code>Expr.arg_min()</code> However except when <code>Null</code> is
ignored <code>Expr.min()</code>, there is a <code>Expr.nan_min()</code>
but no <code>Expr.nan_min()</code>. <code>NaN</code> is sometimes a
value higher than Inf and sometimes regarded as a <code>Null</code>.
Polars conventions <code>NaN</code> \> <code>Inf</code> \>
<code>99</code> \> <code>-99</code> \> <code>-Inf</code> \>
<code>Null</code> <code>Null == Null</code> yields often times false,
sometimes true, sometimes <code>Null</code>. The documentation or
examples do not reveal this variations. The best to do, when in doubt,
is to do test sort on a small Series/Column of all values.

#’ R <code>NaN</code> ~ polars <code>NaN</code> ~ python
<code style="white-space: pre;">\[float(“NaN”)\]</code> #only floats
have <code>NaN</code>s

R <code>Inf</code> ~ polars <code>inf</code> ~ python
<code style="white-space: pre;">\[float(“inf”)\]</code> #only floats
have <code>Inf</code>

<h4>
NULL IS NOT Null is not NULL
</h4>

The R NULL does not exist inside polars frames and series and so on. It
resembles the Option::None in the hidden rust code. It resembles the
python <code>None</code>. In all three languages the
<code>NULL</code>/<code>None</code>/<code>None</code> are used in this
context as function argument to signal default behavior or perhaps a
deactivated feature. R <code>NULL</code> does NOT translate into the
polars bitmask <code>Null</code>, that is <code>NA</code>. R
<code>NULL</code> ~ rust-polars <code>Option::None</code> ~ pypolars
<code>None</code> #typically used for function arguments

<h4>
LISTS, FRAMES AND DICTS
</h4>

The following translations are relevant when loading data into polars.
The R list appears similar to python dictionary (hashmap), but is
implemented more similar to the python list (array of pointers). R list
do support string naming elements via a string vector. In polars both
lists (of vectors or series) and data.frames can be used to construct a
polars DataFrame, just a as dictionaries would be used in python. In
terms of loading in/out data the follow translation holds: R
<code>data.frame</code>/<code>list</code> ~ polars
<code>DataFrame</code> ~ python <code>dictonary</code>

<h4>
Series and Vectors
</h4>

The R vector (Integer, Double, Character, …) resembles the Series as
both are external from any frame and can be of any length. The
implementation is quite different. E.g. <code>for</code>-loop appending
to an R vector is considered quite bad for performance. The vector will
be fully rewritten in memory for every append. The polars Series has
chunked memory allocation, which allows any append data to be written
only. However fragmented memory is not great for fast computations and
polars objects have a <code>rechunk</code>()-method, to reallocate
chunks into one. Rechunk might be called implicitly by polars. In the
context of constructing. Series and extracting data , the following
translation holds: R <code>vector</code> ~ polars
<code>Series</code>/<code>column</code> ~ python <code>list</code>

<h4>
Expressions
</h4>

The polars Expr do not have any base R counterpart. Expr are analogous
to how ggplot split plotting instructions from the rendering. Base R
plot immediately pushes any instruction by adding e.g. pixels to a .png
canvas. <code>ggplot</code> collects instructions and in the end when
executed the rendering can be performed with optimization across all
instructions. Btw <code>ggplot</code> command-syntax is a monoid meaning
the order does not matter, that is not the case for polars Expr. Polars
Expr’s can be understood as a DSL (domain specific language) that
expresses syntax trees of instructions. R expressions evaluate to syntax
trees also, but it difficult to optimize the execution order
automatically, without rewriting the code. A great selling point of
Polars is that any query will be optimized. Expr are very light-weight
symbols chained together.
