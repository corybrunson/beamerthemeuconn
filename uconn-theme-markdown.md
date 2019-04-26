---
title: Beamer themes for the University of Connecticut
author: Jason Cory Brunson, PhD
date: 2019 March 27
aspectratio: 169
institute: |
  Center for Quantitative Medicine, UConn Health
section-titles: false
header-includes: |
  \usepackage[utf8]{inputenc}
  \usepackage[T1]{fontenc}
theme: uconn
themeoptions: campus=health,watermark=oakleaf,logo=side
---

## Markdown + Pandoc

The `uconn` Beamer theme is described in more detail in `uconn-theme-example.pdf`, which is generated from `uconn-theme-example.tex` using all four themes. This slideshow is generated instead from the Markdown file `uconn-theme-markdown.md` using the document conversion program [Pandoc](https://pandoc.org/).

Note that Markdown syntax is not standardized, so much so that i decided not to link to any specific introduction or guide in the previous paragraph. Features may differ between the Pandoc Beamer converter and other engines, so beware that the syntax used here will not necessarily work in, say, GitHub.

# Pandoc Beamer

## Markdown to \LaTeX\ in Pandoc

Render this document directly into a PDF using Pandoc from the command line:

    pandoc uconn-theme-markdown.md \
      -t beamer \
      --include-in-header=environment-shortcuts.tex \
      --toc \
      -o uconn-theme-markdown.pdf

Change the output format to \TeX\ by substituting the final option:

      -o uconn-theme-markdown.tex
      -s

(This will produce an intermediary standalone \LaTeX\ document.)

## Metadata

The [YAML](https://yaml.org/) front matter at the top of `uconn-theme-markdown.md` contains several metadata, including the title, author, institution, and date. This document also sets the following variables:

```yaml
aspectratio: 169
section-titles: false
theme: uconn
themeoptions: campus=health,watermark=oakleaf,logo=side
```

The `theme` variable calls the `uconn` Beamer theme, and the `themeoptions` variables receives options that are passed to the theme.

Find [a list of Beamer-specific variables](https://pandoc.org/MANUAL.html#variables-for-beamer-slides) that can be set in the front matter at the Pandoc User's Guide.

## Environment shortcuts

The Pandoc command above included one atypical option:

      --include-in-header=environment-shortcuts.tex

This adds the contents of `environment-shortcuts.tex` to the \LaTeX\ preamble when rendering. The file contains several definitions like this:

```tex
\newcommand{\blockbegin}[1]{\begin{block}{#1}}
\newcommand{\blockend}{\end{block}}
```

These allow to use \LaTeX\ environments without the use of `\begin{}` and `\end{}`, thereby enabling Pandoc to render Markdown syntax within these environments.

# Formatting text

## Blocks

\blockbegin{Block Title}

This text block is rendered using \verb|\blockbegin{Block Title}| and \verb|\blockend|.
Since Pandoc interprets single carriage returns as spaces, two are required to separate these commands from the text they contain.

\blockend

\theorembegin

Likewise, a theorem can include **bold**, \emph{emphatic}, and `fixed-width` font rendered from Markdown syntax.
Note that \verb|\emph{}| is required for emphatic text when _italics_ are ignored in a theorem block, and notice the difference between `fixed-width` and \verb|inline verbatim code|, which can still be rendered using \verb|\verb|.

\theoremend

## Lists

Enumerated, itemized, and nested lists can be intuitively typed:

```markdown
1. This is a first item.
2. This is a second, but it has
    - not one,
    - not two, but
    - three sub-items.
```

The code above renders as follows:

1. This is a first item.
2. This is a second, but it has
    - not one,
    - not two, but
    - three sub-items.

## Code blocks

The code blocks on the preceding slides use either 4-space indentation (for command line code) or triple–back ticks with syntax highlighting specific to the language on display (`yaml`, `tex`, and `markdown`).

These and many other shorthands are documented in the [Pandoc User's Guide](https://pandoc.org/MANUAL.html).

# Thanks

## Acknowledgments

Since i didn't recognize them in previous documents, i'll thank here the designers of \TeX\ and \LaTeX, as well as those of Markdown and Pandoc, for making this exceedingly easy, while necessarily limited, plain text–to–PDF workflow possible.

As in the other example documents, suggestions are very welcome! Email Cory ([brunson@uchc.edu](mailto:brunson@uchc.edu)), raise an issue, or submit a pull request (on a new branch).

<!--
pandoc uconn-theme-markdown.md \
-t beamer \
--include-in-header=environment-shortcuts.tex \
--toc \
-o uconn-theme-markdown.pdf

-o uconn-theme-markdown.tex \
-s
-->
