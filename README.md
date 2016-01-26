latex-reviewer-diff
===================

Latex package designed to write reviewers response in scientific publications. Provides a system of marks/links between the text and the response. Supports latexdiff.

## Quick-start

1. Place the file `reviewer.sty` in your working directory.

2. Copy your old manuscript `original.tex` into `revised.tex`.

3. Edit `revised.tex` to add the **reviewer** package and answer the comments as in this example (source [here](https://github.com/jealie/latex-reviewer-diff/tree/master/examples)):

```latex
\documentclass{article}

\usepackage{reviewer} %% loads the reviewer package

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

\us
We respectfully disagree with the reviewer's assessment of our work. Nonetheless...

%% Continue ad libitum...
% [...]

%% Ends the review section:
\stopreview\end{DIFnomarkup}

%% From now on, this is the manuscript revised to address the comments:

\maketitle

%% [...]

%% Tag changes that you want to refer with \reviewlabel:
\reviewlabel{explaindetails}The noumena have nothing to do with, thus, the Antinomies. What we
have alone been able to show is that the things in themselves constitute the
whole content of human reason, as is proven in the ontological manuals.

%% [...]

\end{document}
```

4. Compile twice the document:

```bash
pdflatex revised.tex
pdflatex revised.tex # cross-links need two compilations
```


## Advanced usage

+ This package really shines when used in conjunction with [**latexdiff**](https://www.ctan.org/pkg/latexdiff?lang=en):

```bash
latexdiff original.tex revised.tex > diff.tex
pdflatex diff.tex
pdflatex diff.tex # cross-links need two compilations
```

  `diff.pdf` will look like this:

                                                     Page 1 of `diff.pdf`                                                                         |                                                          Page 2                                                                                     
:------------------------------------------------------------------------------------------------------------------------------------------------:|:---------------------------------------------------------------------------------------------------------------------------------------------------:
<a href="url"><img src="https://raw.githubusercontent.com/jealie/latex-reviewer-diff/master/examples/diff_1.png" align="left" width="390px" ></a> | <a href="url"><img src="https://raw.githubusercontent.com/jealie/latex-reviewer-diff/master/examples/diff_2.png" align="right" width="390px" ></a>

  (**latexdif** is useful to highlight automatically the changes between the old `original.tex` and the new `revised.tex`)

+ It is possible to use the option `hide` when loading the package, to generate a final manuscript without the comments:

```latex
\usepackage[hide]{reviewer}
```


## Common problems

+ Many errors arise when you copy reviewer's text that contains special characters. For example:

  * Replace `_` by `` \char`_ ``

  * Put `<` or `>` into `$` signs: `$<$`

  * Escape `#` with `\#`

+ The `\reviewlabel{...}` command doesn't work inside a `\caption{...}`, but it works if you place it just outside:


```latex
\begin{figure}
\includegraphics{...}
\reviewlabel{whatever}
\caption{Some caption}
\end{figure}
```

+ The use of the `DIFnomarkup` environment is not mandatory, but it is solves some rarely occurring issues with **latexdiff**.

Bug reports and pull requests are welcome!
