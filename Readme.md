RegExplain
================

#### *Regular expressions are tricky.* RegExplain *makes it easier to see what you’re doing.*

<!-- [![packageversion](https://img.shields.io/github/description/v/gadenbuie/regexplain.svg)](commits/master) -->

![](https://img.shields.io/badge/lifecycle-maturing-blue.svg) [![Project
Status: Active – The project has reached a stable, usable state and is
being actively
developed.](http://www.repostatus.org/badges/latest/active.svg)](http://www.repostatus.org/#active)
[![CRAN\_Status\_Badge](http://www.r-pkg.org/badges/version/regexplain)](https://cran.r-project.org/package=regexplain)
<!-- [![Last-changedate](https://img.shields.io/badge/last%20change-2020--07--02-yellowgreen.svg)](/commits/master) -->

<!-- Links -->

**RegExplain** is an RStudio addin slash utility belt for regular
expressions. Interactively build your regexp, check the output of common
string matching functions, consult the interactive help pages, or use
the included resources to learn regular expressions. And more.

Inspired by [RegExr.com](https://regexr.com/) and `stringr::str_view()`.

## Installation

Installation is easy with `remotes`

``` r
# install.packages("remotes")
remotes::install_github("gadenbuie/regexplain")
```

## RegExplain in Action

#### Overview

![regexplain
selection](https://raw.githubusercontent.com/gadenbuie/regexplain/af4fe0988a10f34dc528b4d359b80bb06af7809a/docs/regexplain-selection.gif)

#### Regular Expressions Library

![regexplain
library](https://raw.githubusercontent.com/gadenbuie/regexplain/af4fe0988a10f34dc528b4d359b80bb06af7809a/docs/regexplain-library.gif)

#### Try the Built-In Examples

![regexplain
examples](https://raw.githubusercontent.com/gadenbuie/regexplain/af4fe0988a10f34dc528b4d359b80bb06af7809a/docs/regexplain-try-this.gif)

## RStudio Addin

The main feature of this package is the RStudio Addin **RegExplain
Selection**. Just select the text or object containing text (such as the
variable name of a vector or a data.frame column) and run **RegExplain
Selection** from the RStudio Addins dropdown.

<img src="docs/rstudio-addin-list.png" width = "250px;" alt="regexplain in the Rstudio Addins dropdown">

You can also open the addin with `regexplain_gadget()`. This allows you
to pass text or a regular expression to the gadget, which is useful when
you want to work with a regular expression in your code or environment.

``` r
regexplain_gadget(text_vector, "\\b(red|blue|green): \\d{3}")
```

The addin will open an interface with 4 panes where you can

  - edit the **text** you’ve imported
  - build up a **regex** expression and interactively see it applied to
    your text
  - test the **output** of common string matching and replacement
    functions from `base` and `stringr`
  - and refer to a **help**ful cheatsheet

![The panes of regexplain](docs/regexplain-gadget-tabs.png)

When you’re done, click on the **Send Regex to Console** to send your
regex expression to… the console\!

``` r
> pattern <- "\\b(red|orange|yellow|green|blue|purple|white|brown)(?:\\s(\\w+))?"
```

Notice that *RegExplain* handled the extra backslashes needed for
storing the RegEx characters `\b`, `\s`, and `\w`. Inside the gadget you
can use regular old regular expressions as you found them in the wild
(hello, [Stack
Overflow](https://stackoverflow.com/questions/tagged/regex)\!).

### Help and Cheat Sheet

The **Help** tab is full of resources, guides, and R packages and
includes an easy-to-navigate reference of commonly used regular
expression syntax.

![regexplain help windows](docs/regexplain-gadget-help.png)

Open **RegExplain Cheatsheet** from the RStudio Addins drop down to open
the regex reference page in the Viewer pane without blocking your
current R session.

### Import Your Text

There are two ways to get your text into *RegExplain*. The first way was
described above: select an object name or lines of text or code in the
RStudio source pane and run **RegExplain Selection**. To import text
from a file, use **RegExplain File** to you import the text you want to
process with regular expressions.

When importing text, *RegExplain* automatically reduces the text to the
unique entries and limits the number of lines.

![regexplain addins](docs/addin-screenshots.png)

### Regular Expressions Library

The *RegExplain* gadget includes a regular expressions library in the
**RegEx** tab. The library features common regular expressions, sourced
from [qdapRegex](https://github.com/trinker/qdapRegex) and [Regex
Hub](https://projects.lukehaas.me/regexhub), with several additional
patterns.

The full library is stored as a JSON file in
[inst/extdata/patterns.json](/inst/extdata/patterns.json), feel free to
contribute patterns you find useful or use regularly via pull request.

<img src="docs/regexplain-gadget-library.png" height="400px" alt="regexplain library modal">

## View Static Regex Results

*RegExplain* provides the function `view_regex()` that you can use as a
`stringr::str_view()` replacement. In addition to highlighting matched
portions of the text, `view_regex()` colorizes groups and attempts to
colorize the regex expression itself as well.

``` r
text <- c("breakfast=eggs;lunch=pizza",
          "breakfast=bacon;lunch=spaghetti", 
          "no food here")
pattern <- "((\\w+)=)(\\w+).+(ch=s?p)"

view_regex(text, pattern)
```

![Example `view_regex(text, pattern)`.](docs/view-regex.png)

``` r
t_nested <- "anestedgroupwithingroupexample"
r_nested <- "(a(nested)(group(within(group))(example)))"
view_regex(t_nested, r_nested)
```

![Example of nested groups](docs/view-nested.png)

## Notes

Regular expressions are nothing if not a collection of corner cases.
Trying to pass regular expressions through Shiny and HTML inputs is a
bit of a labyrinth. For now, assume any issues or oddities you
experience with this addin are entirely my fault and have nothing to do
with the fine packages this addin is built on. If you do find an issue,
[please file an issue](https://github.com/gadenbuie/regexplain). Pull
requests are welcomed\!
