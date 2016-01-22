latex-reviewer-diff
===================

Latex package designed to write reviewers response in scientific publications. Provides a system of marks/links between the text and the response. Supports latexdiff.

## Quick-start

Place the file `reviewer.sty` in your working directory.

Copy your old manuscript `original.tex` into `revised.tex`.

Add the **reviewer** package and starts answering the comments as in this example:

```latex
\documentclass{article}

% [...]

\usepackage{reviewer} %% loads the reviewer package

% [...]

\begin{document}

%% Starts the review section like so:
\begin{DIFnomarkup}
\startreview 

%% Start copying and pasting the reviewer's comments:
REVIEWER \#1: Can you explain this part a bit further, but without going into detail.

%% Introduce the response with \us. It can contain hyperlinks within the text with \revieweref
\us
We followed this reviewer's advice and updated the manuscript.
See changes at \reviewref{explaindetails}.

%% Introduce more comments with \them
\them
Not sure how to say this diplomatically, but the manuscript is really dull.

%% Continue ad libitum...
\us
We respectfully disagree with the reviewer's assessment of our work. Nonetheless...

% [...]

%% Ends the review section:
\stopreview\end{DIFnomarkup}

%% From now on, this is the new (amended) version of the manuscript

\maketitle

% [...]

%% Tag changes with \reviewlabel:
\reviewlabel{explaindetails}The noumena have nothing to do with, thus, the Antinomies. What we
have alone been able to show is that the things in themselves constitute the
whole content of human reason, as is proven in the ontological manuals.

% [...]

\end{document}
```

You can already compile (twice) this new document, but this package really shines when used in conjunction with [**latexdiff**](https://www.ctan.org/pkg/latexdiff?lang=en):

```bash
latexdiff original.tex revised.tex > diff.tex
pdflatex diff.tex
pdflatex diff.tex # cross-links need two compilations
```

`diff.pdf` will look like this:

<a href="url"><img src="https://raw.githubusercontent.com/jealie/latex-reviewer-diff/master/examples/diff_1.png" align="left" width="400" ></a>
<a href="url"><img src="https://raw.githubusercontent.com/jealie/latex-reviewer-diff/master/examples/diff_2.png" align="right" width="400" ></a>

---

(see also the examples [there](https://github.com/jealie/latex-reviewer-diff/tree/master/examples))

## Advanced usage

It is possible to use the option `hide` when loading the package, to generate a final manuscript without the comments:

```latex
\usepackage[hide]{reviewer}
```

The use of the `DIFnomarkup` environment is not mandatory, but it is solves some rarely occurring issues with **latexdiff**.

## Common problems

Many errors arise when you copy reviewer's text that contains latex special characters. For example:

  * Replace `_` by `` \char`_ ``

  * Put `<` or `>` into `$` signs: `$<$`

The `\reviewlabel{...}` command doesn't work inside a `\caption{...}`, but it works if you place it just outside:


```latex
\begin{figure}
\includegraphics{...}
\reviewlabel{whatever}
\caption{Some caption}
\end{figure}
```

Bug reports and pull requests are welcome!
