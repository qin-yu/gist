# Some Important Configurations in LaTex

- [Some Important Configurations in LaTex](#some-important-configurations-in-latex)
    - [Rules:](#rules)
    - [To solve more than 26 subfigure index:](#to-solve-more-than-26-subfigure-index)
    - [To add bibliography:](#to-add-bibliography)
    - [To keep figures within its section](#to-keep-figures-within-its-section)
    - [To get quote environment](#to-get-quote-environment)
    - [Set space between paragraphs, indentation in first line](#set-space-between-paragraphs-indentation-in-first-line)
    - [`.` in file names causes error](#in-file-names-causes-error)

### Rules:
1. Label should always be after caption in figures
2. With the setting of `[!htb]` you'll get the best results for figure placement
3. Newline(s) between `subfigure` environment breaks side-by-side figures apart
4. `#` has to be escaped, i.e. use `\#`, which is especially common in URLs

### To solve more than 26 subfigure index:
```latex
\usepackage{alphalph}
\renewcommand\thesubfigure{\alphalph{\value{subfigure}}}
```

### To add bibliography:
Biblatex is an easier and more flexible interface and a better language localization than bibtex and natbib.
```latex
\usepackage{biblatex}
\addbibresource{file1.bib}
\addbibresource{file2.bib}

\begin{document}
\printbibliography
\end{document}
```

### To keep figures within its section
After each section:
```
\FloatBarrier
```

### To get quote environment
```latex
\usepackage{csquotes}

\begin{displayquote}
Sé que tengo un ego del tamaño de un planeta pequeño, pero incluso yo a
veces me equivoco
\end{displayquote}
```

### Set space between paragraphs, indentation in first line
```latex
\setlength{\parindent}{0em}
\setlength{\parskip}{1em}
```

### `.` in file names causes error
More than one `.` before file extension?
e.g.
```latex
\includegraphics[width=0.75\linewidth]{figures/figure.0.3.eps}
```
gives error `Unknown graphics extension: .0.3.eps.`

__Solution__
```latex
\usepackage{graphicx}
\usepackage{grffile}
```
