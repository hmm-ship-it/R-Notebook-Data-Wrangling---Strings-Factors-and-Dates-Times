R Notebook
================

``` r
library(tidyverse)
```

    ## ── Attaching packages ────────────────────────────────────────────────────────────────────────────────────────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 3.2.1     ✔ purrr   0.3.2
    ## ✔ tibble  2.1.3     ✔ dplyr   0.8.3
    ## ✔ tidyr   1.0.0     ✔ stringr 1.4.0
    ## ✔ readr   1.3.1     ✔ forcats 0.4.0

    ## ── Conflicts ───────────────────────────────────────────────────────────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
library(stringr)
```

Strings are surrounded by quotes or apostrophes backslash escapes the
character interpretation. This means R won’t use it for syntax,instead
treat it as text \\"

writeLines(x) would output the string excluding control charcters such
as the backslash

\\n is newline

\\t is tab

?‘"’

Multiple strings can be stored in a character vector c(“one”, “two”,
“three”)

str\_length() returns number of characters in a string

``` r
str_length(c("hi", "not", NA))
```

    ## [1]  2  3 NA

to combined strings use str\_c(x, y)

str\_c(“x”, “y”, sep =“,”) separates strings by sep= “x, y”

Missing values don’t play nicely, use str\_replace\_na for them x \<-
c(“abd”, NA) str\_c(“|”, str\_replace\_na(x), “-|”)

using a list within a list in str\_c shorter vectors will be expanded to
match longer vectors str\_c(“pre”, c(“a”,“b”,“c”),“post”) To change a
vector of strings to a single string use collapse str\_c(“x”, “y”, “z”,
collapse =“,”)

x \<- c(“Apple”, “Banana”, “Pear”) parts of string obtained by
str\_sub(x,1,3) \# \> App , Ban, Pea str\_to\_lower(str\_sub(x,1,1)) app
ban pea

str\_to\_upper str\_to\_title etc…

specify locale for inter-operable code via different countries
str\_sort(x, locale =“en”)

1.  The are the same except for a default separator. "" vs " "

2.  sep applies a character/s between strings that are being combined.
    collapse applies a character between a chacracter vector

3.  
<!-- end list -->

``` r
x <- "12345678"
len <- str_length(x)
str_sub(x, ceiling(len/2),ceiling(len/2))
```

    ## [1] "4"

4.  str\_wrap outputs text in paragraph form. You set line width, indent
    and exdent. I would use it to output code that fits on a screen.
    would need to get screen size variables for it to be useful. would
    be handy for console output.
5.  trim removes excessive spacing from the beginning, end, and between
    characters in a string.
6.  str\_c(“a”, “b”, “c”, sep’“,”)

\#Regular Expressions

str\_view() and str\_view\_all()

``` r
x <- c("apple", "banana", "pear")
str_view(x, "an")
```

<!--html_preserve-->

<div id="htmlwidget-52c04c35c9d72f413ca3" class="str_view html-widget" style="width:960px;height:100%;">

</div>

<script type="application/json" data-for="htmlwidget-52c04c35c9d72f413ca3">{"x":{"html":"<ul>\n  <li>apple<\/li>\n  <li>b<span class='match'>an<\/span>ana<\/li>\n  <li>pear<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

<!--/html_preserve-->

``` r
str_view(c("abc","a.c","bef"),"a\\.c")
```

<!--html_preserve-->

<div id="htmlwidget-ade97c96d5f911acd9e6" class="str_view html-widget" style="width:960px;height:100%;">

</div>

<script type="application/json" data-for="htmlwidget-ade97c96d5f911acd9e6">{"x":{"html":"<ul>\n  <li>abc<\/li>\n  <li><span class='match'>a.c<\/span><\/li>\n  <li>bef<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

<!--/html_preserve-->

. matches any character except newline because the escape character is
evaluated twice, once by the string it is in, and once by the REGEX you
need to include a  per function e.g. \\. The period has no special
meaning in a string, so the string feature of r will be confused. It
needs to include another  to say hey strings, this is normal…and then
the REGEX go hey  treat the next special character like its just a
character.

If you try to match a  you need to apply a  per function of str(REGEX())
REGEX needs \\ String then needs a backslash per backslash to pass to
REGEX therefore \\\\

1.First escapse the special meaning of " , second creates a backslash
string but the REGEX it means escape, third escapes the meaning of one
backslash, but the other is still an escape character.

``` r
x <- "\"'\\"
writeLines(x)
```

    ## "'\

``` r
str_view(x, "\"\'\\\\")
```

<!--html_preserve-->

<div id="htmlwidget-0a1e1995e7056bbccdf3" class="str_view html-widget" style="width:960px;height:100%;">

</div>

<script type="application/json" data-for="htmlwidget-0a1e1995e7056bbccdf3">{"x":{"html":"<ul>\n  <li><span class='match'>\"'\\<\/span><\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

<!--/html_preserve-->

``` r
str_view(x, "\"'\\\\")
```

<!--html_preserve-->

<div id="htmlwidget-302fdd969ac08d010abd" class="str_view html-widget" style="width:960px;height:100%;">

</div>

<script type="application/json" data-for="htmlwidget-302fdd969ac08d010abd">{"x":{"html":"<ul>\n  <li><span class='match'>\"'\\<\/span><\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

<!--/html_preserve-->

2.  "'\\\\
3.  This patter will match . anychar . anychar . any char .a.b.c

\#Anchors

Match from start ^ Match from end $

^a apple

a$ Banana

complete string matching ^apple$

use \\b to match boundary between words and non-word characters

``` r
x <- "\"$^$\""
writeLines(x)
```

    ## "$^$"

``` r
str_view(x,"\"\\$\\^\\$\"")
```

<!--html_preserve-->

<div id="htmlwidget-15c319b3a00a2d9e6623" class="str_view html-widget" style="width:960px;height:100%;">

</div>

<script type="application/json" data-for="htmlwidget-15c319b3a00a2d9e6623">{"x":{"html":"<ul>\n  <li><span class='match'>\"$^$\"<\/span><\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

<!--/html_preserve-->

1.  "\\\(\\^\\\)"" To be completely honest escape characters being used
    for both strings and regular expressions makes regular expressions a
    pain in R

2.  str\_view(stringr::words, REGEX\_HERE, match = TRUE) <sup>y x$
    </sup>…$ ^…….

\#matching sets

\\d matches a digit \\s matches any whitespace (space, tab, newline)
\[abc\] matches a b or c \[^abc\] matches anything except a b or c

REGEX special characters $. | ? \* + ( ) \[ { . The above can be used
within \[\] without a backslash

these can’t though \]  ^ and -

1.  str\_view(x, “\[1\]”) str\_view(x, “\[2\]”) str\_view(x,
    “\[^e\]ed\(")  str_view(x, "i[ng|se]\)”)

2.str\_view(x, “ie|\[^c\]ie”) 3.str\_view(x, “q\[^u\]”) 4.???
5.str\_view(x, “\\(\[0-9\]{3,}\\)\[0-9\]{3,}\\-\[0-9\]{4,}”)

``` r
x <- c("(831)559-5555", "()351-4565", "(000)000 0000", "000-(000)-9999")
str_view(x, "\\([0-9]{3,}\\)[0-9]{3,}\\-[0-9]{4,}")
```

<!--html_preserve-->

<div id="htmlwidget-b8af286b27c5445edfe0" class="str_view html-widget" style="width:960px;height:100%;">

</div>

<script type="application/json" data-for="htmlwidget-b8af286b27c5445edfe0">{"x":{"html":"<ul>\n  <li><span class='match'>(831)559-5555<\/span><\/li>\n  <li>()351-4565<\/li>\n  <li>(000)000 0000<\/li>\n  <li>000-(000)-9999<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

<!--/html_preserve-->

? 0 or 1 match + 1 or more match \* 0 or more matches {min,max} if min
or max is missing replace with infinity. If there is only one number
exactly {m}

1.  {,1} {1,} {0,}

2.  match any existing string match any string surrounded by curly
    braces match 4 numbers by 2 by 2 where by is - match 4 back slashes

3.  str\_view(x, “\[3\]{3}”) str\_view(x, “\[aeiou\]{3,}”) str\_view(x,
    “\[^aeiou\]\[aeiou\]{2,}”)

4.  
<!-- end list -->

1.  aeiou

2.  ^aeiou

3.  ^aeiou
